![[Pasted image 20221101124548.png]]
# Amazon Relational Database Service (RDS)

## Supported Engines

- PostgreSQL.
- MySQL.
- MariaDB.
- Oracle.
- Microsoft SQL Server.
- IBM DB2.
- AWS Aurora (MySQL and PostgreSQL compatible).

## Storage Auto Scaling

- Helps to increase storage on RDS instances dynamically.
- You have to set a **Maximum Storage Threshold**. (maximum limit for DB storage).
- Automatically modify storage if:
  - Storage is less than 10% free.
  - Low-storage lasts at least 5 minutes.
  - 6 hours have passed since last modification.

## Read replicas

- Up to 15 Read Replicas.
- Within AZ, Cross AZ or Cross Region.
- Replication is ASYNC. (reads are eventually consistent)
- Replicas can be promoted to their own DB.

### Networking cost

- For RDS Read Replicas within the same region, there is no data transfer cost.

## Multi AZ (Disaster Recovery)

- Increases **availability**.
- SYNC Replication.
- Zero downtime replicating a single AZ DB.
- One DNS name -> automatic failover.

![[rds_multi_az.png]]

## RDS Custom

- Managed Oracle and Microsoft SQL Server with OS and database customization.
- RDS manages the setup, operation and scaling of the DB.
- We can access the underlying EC2 instance using SSH or SSM Session Manager.
- To perform customization -> **De-activate Automation Mode**.

## Backups

- **Automated Backups**:
  - Daily full backup (during the backup window).
  - 1-35 days retention. (0 for no backups)
  - Transaction logs backed-up every 5 minutes.
  - Therefore, you can restore to any point in time within the retention period.
- **Manual DB Snapshots**:
  - Manually triggered by the user.
  - Retention is indefinite until deleted.
  - Useful for when you have to stop a DB. (so you don't get charged for the storage)

### Restore Options

- Restore a RDS from a backup or snapshot -> creates a **new DB**.
- To **restore a MySQL RDS database cluster from S3**:
  - Create backup of on-premise db.
  - Store it on S3.
  - Restore it to a new RDS instanc runing MySQL.

## Security

- **Encryption at rest**:
  - Using KMS. Must be defined at launch time.
  - If the master is not encrypted, the read replicas cannot be encrypted.
  - To encript an unencrypted DB: create Snapshot -> restore as encrypted.
- **Encryption in flight**: TLS by default.
- **IAM Authentication**: Use IAM Roles to connect (instead of passwords).
- **Security Groups**: Control access to the DB.
- **No SSH available**. (except for RDS Custom).
- **Audit Logs can be enabled**. Send to Cloudewatch for longer retention.
 
