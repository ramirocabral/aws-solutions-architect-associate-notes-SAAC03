![[Pasted image 20221031091542.png]]

## TLDR
Server which grants and manager access to an application running in AWS. This is archived by granting an authenticated user temporary [[IAM]] credentials.

## Cognito User Pools

- Sign in functionality for app users.
- Serverless database of users for web and mobile apps.
- Simple login, password reset, email verification, MFA, Oauth, etc.

### Integrations

CUP integrates with [[APIGateway]] and ALB.

![[cognito_api_gateway.png]]

## Identity Pools

- Get identities for "users" so they obtain temporary AWS credentials.
- Users source can be Cognito User Pools, 3r party, etc.
- Users can access the AWS services directly or through [[APIGateway]].
- IAM Policies are defined in Cognito.
- Default IAM roles for authenticated and guests users.

### Row Level Security in DynamoDB

- Users can only access their own data. (rows)
