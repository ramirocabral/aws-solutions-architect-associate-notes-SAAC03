![[Pasted image 20221101172817.png]]
# Cloudformation

## TLDR

Templates to create [[VPC]] and almost any resource in AWS. Allows to create Infrastructre as Code.

## Features

- IaC.
- Most resources are supported.
- Declarative programming.
- Can see visually see the resources with Infrastructure Composer.
- Template versions are stored in [[S3]].

## Cloudformation StackSets

- Create stacks in AWS accounts across regions using a single template.
- Use the template as the basis for provisioning stacks.
- Use with [[AWSOrganizations]].

## Creation Policies

- **`CreationPolicy`** means a resource has to be up an running for the next step to continue

## Service Role

- IAM Role that allows CloudFormation to create/update/delete stack resources on your behalf.
- Give ability to users to create/update/delete stack resources even if they don't have the permissions to work with those resources.
- User must have **iam:PassRole** permission.


## Instance Scheduler

- Deployed through CloudFormation.
- **Automatically start/stop your AWS sevices to reduce costs**. (up to 70%)
- Example: stop company EC2 instances outside business hours.
- Supports [[EC2]] instances, [[ASG]], [[RDS]] instances.
