![[Pasted image 20221101130307.png]]
# Eastic File System

## TLDR 

High performance network file system which is pay per gb use and can attach to multiple services in multiple AZs.

## Features
- Multi AZ.
- High avalilable, scalable and expensive.
- Pay per use.
- Uses [[SecurityGroup]].
- Compatible with Linux AMIs. (NOT WINDOWS).
- Encryption at rest with [[KMS]].

## Performance

- 1000s of clients 10GBs throughput.
- Can handle petabyte scale data.

- **Performance modes**:
  - General purpose (default).
  - Max I/O.
- **Throughput modes**:
  - Bursting (default).
  - Provisioned.
  - Elastic: Scales throughput automatically based on workloads.

## Storage classes

### Storage Tiers

Lifecycle policies available for cost savings.

- **Standard**: Frequently accessed files.
- **Infrequent Access (EFS-IA)**: cost to retrieve files but lower storage costs.
- **Archive**: rarely accessed data.

### Availability and durability

- **Standard**: Multi-AZ, great for prod.
- **One Zone**: One AZ, great for dev, compatible with IA (EFS One-Zone IA).
