![[Pasted image 20221102195508.png]]

## TLDR

Ml based continuous monitoring and thread detection service. Helps for Crypto exploits

## Features

- Threat detection 
- Continously monitor AWS Accounts, workload and data stored in [[S3]].
- Integrates with thread intelligence (known bad IPs).
- Uses ML to give insight.
- Protection against crypto currency attacks.

## Source to Analyse

- [[CloudTrail]] Managment Events.
- [[CloudTrail]] [[S3]] Data events.
- [[VPC]] Flow Logs.
- DNS Logs.
- [[EKS]] Audit Logs.

## Findings

- [[CloudWatch]] Event Rules to [[Lambda]] or [[SNS]].
- If you disabled the service it will reset the service and delete all data collected.

![[guardduty.png]]
