![[Pasted image 20221101120425.png]]

## TLDR
Kinesis is a set of services for streaming real time or next to real time data in AWS. Its generaly more expensive and more difficult to setup than [[SQS]] but offers more features and higher performance.

- **Producers**: Applications/Kinesis Agents.
- **Consumers**: Applications/Lambdas/Data Firehose/Service for Apache Flink.

## Features
- Collect and store streaming data in **real-time**.
- Retention up to 1 year.
- Reprocess (replay) data by consumers.
- Data can't be deleted (until it expires).
- Data up to 1MB.
- Data ordering guarantee for data with the same "Partition ID"
- At-rest KMS encryption, in-flight HTTPS encryption.

## Capacity Modes

- **Providioned mode**:
  - Choose number of shards.(1 shard = 1MB/s in, 2MB/s out)
  - Scale manually to increase/decrease shards.
  - Pay per shard providiones per hour.
- **On-demand mode**:
  - No need to provision.
  - Default capacity: 4 MB/s in.
  - Scales based on observed throughput peak during last 30 days.
  - Pay per stream per hour and data in/out per GB.


