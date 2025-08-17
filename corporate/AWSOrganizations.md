![[Pasted image 20221031085836.png]]

## TLDR
This is a service to manage multiple accounts and big user count at a central place. Also has features regarding pricing and setting standards.

## Features

- Global service.
- Manage multiple accounts.
- Main accounts -> management account.
- Other accoutns -> member accounts. (can only be part of one organization)
- **Consolidated Billing** actoss all accounts.
- Pricing benefits from aggregated usage (volume discount for EC2, S3, etc.).
- **Shared reserved instances and Savings Plans** across accounts.
- API to automate AWS account creation.

![[organizations_example.png]]

## Advantages

- Multi Accounts vs One Account Multi VPC
- **Tagging standards** for billing purposes.
- Enable CloudTrail across all accounts, send logs to central S3 account.
- Send CloudWatch logs to central logging account.
- Establish Cross Account Roles for Admin purposes.

### SCP (Service Control Policies)

- IAM policies applied to OU or Accounts to restrict Users and Roles. (don't apply to management account)
- An account must have an explicit allow from the root through each OU in the direct parth. (does not allow anything by default)

![[organizations_policies.png]]

## Tag Policies

- Standardize tags across accounts.
- Define tag keys and allowed values.
- Helps with Cost Allocation Tags and Attribute-based Access Control.
- Generate a report that lists all tagged/non-compliant resources.
- Can use [[EventBridge]] to monitor non-compliant tags.

## IAM Conditions
