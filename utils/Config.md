![[config.png]]

## Overview

- Audit and record **compliance** of AWS resources.
- Record configurations and changes over time.
- Per-region service.
- Can be aggregated across regions and accounts.
- Questions that can be solved:
  - Is there unrestricted SSH access to my SGs?
  - Do my buckets have any puyblic access?
  - ...
- Can receive alerts ([[SNS]]) for any changes.
- Can store the configuration data on [[S3]] (analyzed by [[Athena]]).

## Config Rules

- Can use AWS managed config rules (over 75).
- Can make custom rules using [[Lambda]] functions.
- Example:
  - Each EBS is of type gp2.
  - Each [[EC2]] instance is t2.micro.
- Rules can be evaluated/triggered.
  - For each config change.
  - For regular time intervals.
- **Rules do not prevent actions from happening**.

### Notifications

- Use EventBridge to trigger notifications when AWS resources are non-compliant.

![[config_notifications.png]]

## Remediations

- Automate remediation of non-compliant resources using [[SSM]] Automation Documents.
- Use AWS-managed Automation Documents or create custom ones.
- Can set **Remediation Retries**.

![[config_remediations.png]]
