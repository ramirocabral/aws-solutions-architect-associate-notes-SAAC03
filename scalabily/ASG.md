![[Pasted image 20221101113842.png]]
# Auto Scaling Group

- Scale OUT/IN EC2 instances.
- We can have a min and a max number of instances running.
- Automatically register instances with a [[ELB]].
- Recreate an instance if it is unhealthy (health checks can also be made with an ELB).
- They are FREE, you pay only for the underlying instances.
- You specify a launch template, min, desired and max capacity and Scaling Policies.

## Launch template

Similar to launch config (deprecated).

Specifies:

- AMI + instance type.
- EC2 user data.
- EBS volumes.
- Security groups.
- Key pairs.
- IAM roles.
- Network + subnet information.
- Load Balancer information.

## Auto Scaling

It is possible to scale based on [[CloudWatch]] alarms. The alarms monitor metrics and they can trigger scaling.

## Scaling Policies

### Dynamic Scaling

- **Target Tracking Scaling**: Scale to match a target metric (e.g. 50% CPU).
- **Simple/Step Scaling**: React based on CloudWatch alarms.

### Scheduled Scaling

- Scale on predefined time window.
- Anticipate load changes.

### Predictive Scaling

Continuously forecast load and schedule scaling ahead.

## Good metrics to scale on

- CPUUtilization: average CPU usage across instances.
- RequestCountPerTarget: to make sure the number of requests per instance is stable.
- Average Network In/Out: to make sure the network is not saturated. Network-bound apps.
- Any custom metric (using [[CloudWatch]]).

## Scaling Cooldown

- After a scaling activity -> Cooldown Period (default 300s).
- The ASG won't launch or terminate instances during this period. (metric stabilization).
