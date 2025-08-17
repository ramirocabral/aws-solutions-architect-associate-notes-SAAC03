![[Pasted image 20221101121751.png]]

## Overview

- **Automatic Security assessments.**
- Continuous scanning of infrastructure.
- Package vulns (audit).
- Uses database of CVE.
- Generates Risk Score.

## [[EC2]]

- Uses [[SSM]] agent.
- Analyze against **unintended network accessibility**.
- Analyze running OS against known vulns.

## Containers pushed to ECR

- Assessment on containers on push.

## [[Lambda]] Functions

- Identifies software vulnerabilities in function code and package dependencies.
- Assessment of functions as they are deployed.

## Integration

- AWS Security Hub.
- Send events to [[EventBridge]].
