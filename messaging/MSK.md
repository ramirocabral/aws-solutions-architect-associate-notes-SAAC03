
## Overview

- Alternative to [[Kinesis]].
- Fully managed Apache Kafka cluster on AWS.
- Deploy cluster in a VPC, multi-AZ.
- Data stored in [[EBS]] volumes as long as you want.

## MSK Serverless

- No provisioning.
- Automatic scaling.

## Diffrence to Kinesis

![[msk_kinesis.png]]

## Consumers

- [[Flink]].
- [[Glue]].
- [[Lambda]].
- Custom consumer on [[EC2]], [[ECS]], [[EKS]], etc.
