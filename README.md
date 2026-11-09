# AWS Network Foundation

A hands-on learning project on AWS, built in phases. It starts with a secure account and a network built by hand, then recreates that infrastructure as code with Terraform.

> This is a personal learning project, not a production system.

## Project phases

| Phase | Goal | Status |
|---|---|---|
| 0 | Secure AWS account baseline | Done |
| 1 | Network built manually: VPC, subnets, Internet Gateway, route tables, Security Groups, EC2 with SSH | Planned |
| 2 | Recreate Phase 1 with Terraform, with remote state in S3 | Planned |
| 3 | Private application behind an ALB, with NAT, an IAM role and CloudWatch | Planned |
| 4 | GitHub Actions: `terraform fmt`, `validate` and `plan`, using OIDC and no automatic apply | Planned |
| 5 | Run a container image from Amazon ECR on EC2 | Planned |
| 6 | Final documentation and AWS Solutions Architect Associate certification | Planned |

## How I work

1. Understand the cloud resource.
2. Create it manually.
3. Understand how it works.
4. Recreate it with Terraform.
5. Document what I learned.

## Cost rules

- Keep a budget alert active on the account.
- Delete the resources at the end of every session.

## Public repository reminder

This repository is public. Never commit account IDs, email addresses, access keys, or screenshots with sensitive data.

## Documentation

- [Phase 0: account baseline](docs/phase-0-account-baseline.md)
- [Troubleshooting log](docs/troubleshooting-log.md)
