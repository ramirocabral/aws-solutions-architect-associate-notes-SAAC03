![[redshift.webp]]

# Overview

- Based on PostgreSQL, but not used for OLTP.
- It's OLAP (Online Analytical Processing).
- 10x better performance than other data warehouses.
- Scales to PBs of data.
- Columnar storage.
- Two modes: Provisioned and Serverless.
- SQL interface for performing queries.
- BI tools such as [[Quicksight]] or Tableau integate with it.

## Redshift Cluster

- Leader node: query planning, results aggregation.
- Compute node: perform the query, send results ro leader.
- Provisioned mode:
  - Choose instance types in advance.
  - Can reserve instances for cost savings.

![[redshift_architecture.png]]

## Snapshots & DR

- **Multi-AZ mode for some clusters.**
- Snapshots are stored in [[S3]].
- Snapshots are incremental. (only what has changed is stored).
- Can restore a snapshot into a **new cluster**.
- Can be automated, or manual (retained until you delete it).
- **Can configure it to automatically copy snapshots of a cluster to another region.**

