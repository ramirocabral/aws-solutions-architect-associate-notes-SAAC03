![[Pasted image 20221031085227.png]]
# Directory Service

## TLDR

A collection of sub services which allows companies to leverage directory authentication within AWS. Supports Microsoft Active Directoy.

## Versions

### AWS Managed Microsoft AD

- Create your own AD in AWS, manage users locally, supports MFA.
- Establish "trust" connectinos with on-premise AD.

### AD Connector

- Directory Gateway (proxy) to redirect to on-premise AD, supports MFA.
- Users managed on the on-premise AD.

### Simple AD

- AD-compatible managed directory on AWS.
- Cannot be joined with on-premise AD.
