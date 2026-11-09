# Phase 0: Account Baseline

Goal: prepare an AWS account that is safe to use for the rest of the project.

**Status:** Done (November 9, 2026)
**Default region:** `us-east-1`

## Checklist

- [x] Enable MFA on the root user, because root has full control of the account.
- [x] Stop using root for daily work, to limit the impact of a mistake or a leaked credential.
- [x] Create an administrator identity with IAM Identity Center or IAM, with MFA, for day-to-day access.
- [x] Create a USD 5 budget alert, to detect unexpected costs early.
- [x] Review the AWS free plan: credits, duration of up to 6 months, and what happens when it ends, to avoid surprises.
- [x] Install the AWS CLI and configure access without leaving keys in this repository, so credentials are never exposed.

## What I configured

| Area | Configuration |
|---|---|
| Account plan | Upgraded from the expired Free plan to the Paid plan. USD 100 of Free Tier credits remain and apply automatically to bills. |
| Root user | MFA enabled. No access keys. IAM access to billing information enabled. Used only for root-only tasks. |
| Admin group | `Admins`, with the AWS managed policy `AdministratorAccess`. |
| Admin user | IAM user `delfi-admin`, member of `Admins`, console access, MFA enabled, no access keys. |
| Cleanup | Deleted an unused IAM user that had `AdministratorAccess` and active access keys. |
| Budget | Monthly cost budget of USD 5. Email alerts at 85% and 100% of actual spend, and at 100% of forecasted spend. |
| AWS CLI | AWS CLI v2 (2.32.0 or later). Authenticated with `aws login`, which issues temporary credentials. No `~/.aws/credentials` file. |

Verification:

```powershell
PS> aws sts get-caller-identity
{
    "UserId": "AIDA...",
    "Account": "XXXXXXXXXXXX",
    "Arn": "arn:aws:iam::XXXXXXXXXXXX:user/delfi-admin"
}

PS> Test-Path $HOME\.aws\credentials
False
```

## Decisions

### Paid plan instead of a new Free plan account

The Free plan closes the account after 6 months or when the credits run out, whichever comes first. This project runs for longer than that, and its resources need to survive. The Free Tier is also only for new customers, so a second account would not be eligible. The Paid plan has no monthly fee: I pay only for what I use, the remaining credits are applied first, and the budget alert controls the risk.

### IAM user instead of IAM Identity Center

IAM Identity Center is the recommended way to give people access to AWS. However, access to AWS accounts through Identity Center requires AWS Organizations. For a single lab account, a dedicated IAM admin user with MFA and no access keys is simpler. If the project grows to several accounts, I will move to Identity Center with Organizations.

### Permissions through a group

Permissions are attached to the `Admins` group, not directly to the user. They are managed in one place and inherited by every member.

### `aws login` instead of access keys

Access keys are permanent credentials: if they leak, they work until someone deletes them. `aws login` uses my console sign-in (with MFA) and gives the CLI temporary credentials that refresh automatically, with a session of up to 12 hours. No long-term secret is stored on my machine or in this repository.

## What I learned

- The AWS account and the root user are different things: the account is the container, and root is its single all-powerful identity. Root can't be deleted or limited with IAM policies.
- Some tasks can only be done as root, such as enabling IAM access to billing information. Without that, even an admin with `AdministratorAccess` can't see billing.
- Temporary credentials are safer than permanent ones. This decides between a role and a user, and between `aws login` and access keys.
- Unused identities with long-term credentials are a real risk, so I review them and delete them.
- When the Free plan expires, the account is suspended and AWS keeps its content for 90 days. Upgrading to the Paid plan within that window restores access.
- `AdministratorAccess` is broad. It is acceptable for a personal admin user, but it does not follow least privilege.

## Next improvements

- [ ] Replace `AdministratorAccess` with narrower permissions as I learn what I need.
- [ ] Enable CloudTrail to audit account activity.
- [ ] Review findings in IAM Access Analyzer.
