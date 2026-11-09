# Troubleshooting Log

One entry per real problem found during the labs.

## Template

### Entry title

- **Symptom:**
- **Hypothesis:**
- **Diagnosis:**
- **Cause:**
- **Solution:**
- **What I learned:**

---

## Phase 0

### AWS account suspended after the Free plan ended

- **Symptom:** after signing in as root, the console showed "Your AWS account is suspended, please contact customer support".
- **Hypothesis:** the end of the Free plan.
- **Diagnosis:** an email from AWS Billing said the account had been closed because the 6-month Free plan period had ended. AWS Support confirmed it and said there were still Free Tier credits left.
- **Cause:** the account had been created months earlier on the Free plan and never used. The Free plan closes the account after 6 months or when the credits run out, whichever comes first.
- **Solution:** upgraded the account to the Paid plan within the 90-day window (Billing and Cost Management → Upgrade plan). The account was restored with USD 100 in credits.
- **What I learned:** the Free plan never charges you, but it closes the account. To keep long-lived lab resources, the Paid plan plus a budget alert is the safer setup.

### Unused IAM user with admin permissions and access keys

- **Symptom:** while creating the admin user, I found an old IAM user that I didn't remember creating.
- **Hypothesis:** a leftover from an earlier tutorial.
- **Diagnosis:** the user had `AdministratorAccess`, MFA and active access keys, and had never signed in to the console.
- **Cause:** created during an earlier attempt and never cleaned up.
- **Solution:** deleted the user, which also deleted its access keys. I checked that there was no `~/.aws/credentials` file with those keys on my machine. I created a new admin user with no access keys.
- **What I learned:** forgotten identities with permanent credentials are an easy attack surface. Review users, permissions and keys regularly, and remove anything unused.
