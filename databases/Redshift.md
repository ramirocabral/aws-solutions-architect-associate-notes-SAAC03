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

## Redshift Spectrum

- Query data that is already in S3 without loading it.
- **Must have a Redshift cluster available to start the query**.
- The query is then submited to thousands of Redshift Spectrum nodes.
- Uses [[Glue]] Data Catalog under the hood.

## Snapshots & DR

- **Multi-AZ mode for some clusters.**
- Snapshots are stored in [[S3]].
- Snapshots are incremental. (only what has changed is stored).
- Can restore a snapshot into a **new cluster**.
- Can be automated (set retention), or manual (retained until you delete it).
- **Can configure it to automatically copy snapshots of a cluster to another region.**

## Loading data

- **Large inserts are MUCH better**.
- With Kinesis Data Firehose.
- With S3 using COPY command. (through Internet or Enhanced [[VPC]] Routing).
- With the JDBC driver in an EC2 instance.
