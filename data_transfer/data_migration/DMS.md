![[Pasted image 20221031103642.png]]

## TLDR

Migrate an exsisting database into another one. Can also do DB shema conversion.

## Features

- Seamlessly migrate.
- Full set.
- Resilient.
- Self healing.
- Data change capture.
- No code needed.
- Replication instaces for scaling workloads.
- Homogeneous and heterogeneous migrations.
- Support continous repication.
- Needs an [[EC2]] instance to run DMS software.
- If target is [[S3]] it generates CSV.
- Can use in transit encrypt by adding ca cert to endpoint.

## Sources

- [[EC2]] instances. (running a db)
- On premise databases.
- Azure.
- [[S3]].
- [[Aurora]].
- [[RDS]].
- [[DocumentDB]].

## Targets

- On-premise and [[EC2]] instances.
- [[RDS]].
- [[Redshift]].
- [[DynamoDB]].
- [[DocumentDB]].
- [[OpenSearch]].
- [[Neptune]].
- Data Warehouses.
- Streaming Platforms.
- [[Kinesis]].
- Amazon Manged Streaming of Kafka [[MSK]].

## Multi-AZ Deployment

- DMS provisions and mantains a synchronously stand replica in a different AZ.

## Schema Conversion Tool 

- Convert DB's schema from one engine to another.
- No need when migrating the same engine.
