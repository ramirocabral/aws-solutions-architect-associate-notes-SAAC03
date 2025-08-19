![[Pasted image 20221102200252.png]]

## TLDR

Firewall for a [[VPC]].

## Features

- 1000s of rules.
- From L3 to L7.
- VPC to VPC, outbound, inbound, DX and VPN.
- Protocol rules.
- Stateful domain list group (e.g. only allow traffic to *.google.com).
- Rules can be centrally managed by [[FireWallManager]].
- General pattern matching using regex.
- Send logs to [[S3]], [[CloudWatch]] , or [[DataFirehose]].

## Filter

- Allow.
- Drop.
- Alert.

## Active flow inspection

- Intrusion preventions (Managed by AWS).
