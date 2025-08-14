![[Pasted image 20221101212132.png]]

## TLDR
NoSQL Serverless DB. Tons of features and can be global.

## Features

- Fully managed, highly available with replication across multiple AZs.
- Scales to massive workloads.
- Key-Value.
- Milisec latency.
- Auto-scaling capabilities.
- Standard and Infrequent Access Table classes.
- **TTL** -> automatically delete items after an expiry timestamp.

## Basics

- Each table has a **primary key**.
- Each table can have an infinite number of items (rows).
- Each item has **attributes**.
- Max item size 400KB.
- Supported data types:
  - Scalar Types.
  - Document Types (list, map).
  - Set Types.
- You can **rapidly evolve schemas**.

## R/W Capacity Modes

- **Provisioned Mode** (default)
  - Specify number of r/w per second.
  - Pay per provisiones Read Capacity Units (RCU) and Write Capacity Units (WCU).
  - Possibly to add auto-scaling.
- **On-Demand Mode** 
  - R/W automatically scale up/down.
  - No planning needed.

## DynamoDB Accelerator (DAX)

- Fully-managed, highly available, in-memory cache for DynamoDB.
- **Microseconds latency for cached data**.
- Does not require application logic modification.
- Default: 5 minutes cache TTL.

## Stream Processing

- Ordered stream of item-level modifications in a table.
- Use cases:
  - Reacts to changes in real-time.
  - Real-time usage analytics.
  - Insert into derivative tables.
  - Cross-region replication.
  - Invoke Lambdas on changes to tables.

### DynamoDB Streams

- 24h retention.
- Limited # of customers.
- Process using Lambda Triggers, or DynamoDB Stream Kinesis Adapter.

### Kinesis Data Streams

- (up to) 1 year retention.
- High # of consumers.
- Process using [[Lambda]], [[Kinesis]] Data Analytics, [[DataFirehose]], [[Glue]], etc.

## Global Tables

- Multi-region, fully replicated tables.
- Two-way replication.
- Make a DDB table accessible with **low latency** in multiple-regions.
- Active-active replication.
- Can Read/Write to table in any region.
- Must enable DDB Streams as pre-requisite.

## Backups

- Continuous backups using point-in-time recovery (PITR).
  - Recover to any time within the backup window.
- On-demand backups.
  - Long term, until explicitly deleted.
  - Doesn't affect performance.
  - Can be configured with AWS Backup.

## Integration with [[S3]]

- **Export to S3** (must enable PITR).
  - Works for any point in time in the last 35 days.
  - Doesn't affect the read capacity of the table.
  - Export in DDB JSON or ION.
- **Import from S3**.
  - Import CSV, DDB JSON or ION files.
  - Does not consume write capacity.
  - Creates a new table.
