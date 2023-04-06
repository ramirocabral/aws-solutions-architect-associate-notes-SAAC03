![[Pasted image 20221101172817.png]]
# Cloudformation

## TLDR
Templates to create [[VPC]] and almost any resource in AWS. Allows to create Infrastructre as Code.

## Features
- IaC
- most resources are supported
- Template versions are stored in [[S3]]

## Cloudformation StackSets
- create stacks in AWS accounts across regions using a single Template
- use the template as the basis for provisioning stacks
- use with [[AWSOrganisations]]

## Creation Policies
- **`CreationPolicy`** meanx a resource has to be up an running for the next step to continue