# Phase 0: Account Baseline (Plan)

Goal: prepare an AWS account that is safe to use for the rest of the project. Nothing on this list has been done yet.

## Checklist

- [ ] Enable MFA on the root user, because root has full control of the account.
- [ ] Stop using root for daily work, to limit the impact of a mistake or a leaked credential.
- [ ] Create an administrator identity with IAM Identity Center or IAM, with MFA, for day-to-day access.
- [ ] Create a USD 5 budget alert, to detect unexpected costs early.
- [ ] Review the AWS free plan: credits, duration of up to 6 months, and what happens when it ends, to avoid surprises.
- [ ] Install the AWS CLI and configure access without leaving keys in this repository, so credentials are never exposed.

## Decisions

_To be completed._

## What I learned

_To be completed._
