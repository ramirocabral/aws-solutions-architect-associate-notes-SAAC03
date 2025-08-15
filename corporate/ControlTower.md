![[Pasted image 20221031092405.png]]
# AWS Control Tower

## TLDR
Control Tower is often used in conjunction with [[AWSOrganizations]]
to manage and configure a multi account setup.

## Benefits
- Automate setup of [[AWSOrganizations]]
- Automate policy management using guard rails
- Detect policy viloations
- Monitor compliance through dashboard
- Streamline account creation in [[AWSOrganizations]]

## Guardrails

### Preventive Guardrail
- uses [[AWSOrganizations]] SCP
- e.g. restrict regions across all accounts

### Detective Guardrail
- uses [[AWSConfig]]
- e.g. identify untagged resources

## Further Integration
- [[SNS]]