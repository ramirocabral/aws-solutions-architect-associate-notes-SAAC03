## Overview

- Only allow rules.
- Refrence IP or other SG.
- Essential a firewall.
- Access to ports.
- Authorized IP ranges.
- Inbound and outbound.
- One group to many instances.
- [[VPC]] and region bound.
- Use seperate sg for ssh access.
- Time out usually means sg issue.
- Connection refused application or server error.
- Default all inbound is blocked all outbound allowed.
- Stateful, if traffic is allowed out its allowed back in.
- Targets:
  - [[EC2]] instances. (ENIs)
  - ALB.
  - [[RDS]] and [[Aurora]].
  - [[ElastiCache]].
