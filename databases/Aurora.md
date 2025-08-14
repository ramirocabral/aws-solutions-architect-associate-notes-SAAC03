![[Pasted image 20221101210837.png]]
# Amazon Aurora

## TLDR
AWS custom DB engine, very high performant. Useful for global and serverless relational database applications.

## Features

- Compatible with MySQL and Postgres.
- 5x faster than MySQL.
- 3x faster than Postgres.
- Storage automatically grows in incrementes of 10GB up to 128TB.
- Can have up to 15 replicas, with replication faster than MySQL.
- Instantaneous failover.
- Costs more than RDS (~ 20% more), but it's more efficient.

## High Availability and Read Scaling

[Useful Article](https://aws.amazon.com/blogs/database/understand-amazon-aurora-high-availability-and-disaster-recovery-from-an-oracle-perspective/)

- Aurora stores 6 copies of your data across 3 AZs.
  - Needs 4 healthy copies out of 6 for writes.
  - Needs 3 healthy copies out of 6 for reads. (kind of a RAID configuration)
  - Self healing with peer-to-peer replication.
- One Aurora Instance takes writes (master).
- Master + up to 15 Aurora Replicas serve reads. By default only one master.
- Supports cross-region replication.
- Automated failover for master in less than 30 sec.

*Basically, Aurora separates the compute and the storage layers.
The storage layer is distributed across three AZs, with 6 copies of the data.*

![[aurora_design.png]]

## Aurora Clusters

- **Writer Endpoint** -> points at the current master.
- **Reader Endpoint** -> connection load balancing, automatically connects to the read replicas.
- There is auto-scaling for the replicas.

![[aurora_cluster.png]]

## Custom Endpoints

- Define a subset of Aurora instances as a Custom Endpoint.
- E.g run analytical queries on specific replicas.
- The Reader Endpoint generally not used after defining Custom Endpoints.

## Aurora Serverless

- Automated database instantiation and auto-scaling based on actual usage.
- Pay per second, can be more cost-effective.

## Aurora Global Database

- 1 Primary Region. (r/w cluster)
- Up to 5 secondary Read-only Regions. (read clusters)
- Up to 16 read replicas per secondary region.
- **Cross-region replication** takes less than 1 second.

## Aurora Machine Learning

- Add ML-based prediction to apps using SQL.
- Suports Sagemaker, Comprehend.
- You don't need to have ML expertise.

## Babelfish

- Allows Aurora PostgreSQL to understand MS SQL Server commands.
- First, you have to migrate the DB to Aurora PostgreSQL. (using DMS)


## Aurora Backups

- **Automated Backups**:
  - 1-35 days retention. (cannot be disabled)
  - point-in-time restore in that timeframe.
- **Manual DB Snapshots**:
  - Manually triggered by the user.
  - Retention is indefinite until deleted.

### Restore Options

- Restore a Aurora DB from a backup or snapshot -> creates a **new DB**.
- To **restore a MySQL Aurora Cluster from S3**:
  - Create backup of on-premise db using **Percona XtraBackup**.
  - Store it on S3.
  - Restore it to a new RDS instance runing MySQL.

## Aurora Database Cloning

- Create a clone of an Aurora cluster.
- Useful for testing and development. Faster than snapshot and restore.
- Uses **copy-on-write** technology.

## Security

Shared with [[RDS]].

## RDS Proxy

- Fully managed, highly available database proxy.
- **Improves DB efficiency**, reduces the stress on the DB and minimizes open connections.
- Reduced RDS and Aurora failover time by up to 66%.
- No code changes required.
- Enforce IAM authenticacion for DB, and securely store credentials in AWS Secrets Manager.
- **Never public accesible**. Must be accessed from a VPC.
