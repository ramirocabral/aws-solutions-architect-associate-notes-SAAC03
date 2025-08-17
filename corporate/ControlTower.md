![[Pasted image 20221031092405.png]]

## TLDR

Control Tower is often used in conjunction with [[AWSOrganizations]] to manage and configure a multi-account setup.

## Benefits

- Easy way to **set up and govern** a seure and compliant multi-account AWS enviroment based on best practices.
- Automate policy management using guard rails.
- Detect policy violations and remediate them.
- Monitor compliance through dashboard.
- Streamline account creation in [[AWSOrganizations]].

## Guardrails

Ongoing governance for your Control Tower enviroment.

### Preventive Guardrail

- Uses [[AWSOrganizations]] SCP.
- e.g. restrict regions across all accounts.

### Detective Guardrail

- Uses [[Config]].
- e.g. identify untagged resources.

## Further Integration

- [[SNS]]
