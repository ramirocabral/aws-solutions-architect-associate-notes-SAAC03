![[Pasted image 20221031085836.png]]
# AWS Organisations

## TLDR
This is a service to manage multiple accounts and big user count at a central place. Also has features regarding pricing and setting standards.

## Features
- Group multiple AWS accounts
- Global service
- Manage multiple accounts
- There is one main account which is the root, the other accounts  join the [[AWSOrganizations]] of the root account as member accounts
- Shared resources possbile (See [[VPC]])
- You can leverage the API to quickly create new AWS accounts
- Can use a central [[S3]] account for logs
- Central audit account

## Limitations
- A single account can not be in two diffrent organisations

## Cost Management
- Consolidated billing makes monthly fees for some resources, which are used by multiple accounts within the [[AWSOrganizations]], only be payed once (E.g. [[AWSShield]])
- Benefits for aggregated usage of resources and services
- Share reserved [[EC2]] instances and savings plans between your AWS  accounts


## Structure
![[Pasted image 20221031091158.png]]

### Serve Control Policies (SCP)
- [[IAM]] Policies for Account Groups (OUs)
- Affect all users even the root user
- Dont affect service linked policies (like [[S3]] bucket policy)
- use for denies cross account in your org
