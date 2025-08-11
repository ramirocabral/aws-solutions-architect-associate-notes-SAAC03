![[Pasted image 20221031110419.png]]
# Storage Gateway

## TLDR

Can be used for a Hybrid Cloud setup, data is produced on-premise and synced to AWS.

## Usage

- Long term migrations.
- Security.
- Disaster recovery.
- Complicance.
- Tiered storage.
- Backup and restore.

## Gateway Types

### [[S3]] File Gateway

- NFS or SMB Protocol.
- Translates file request to HTTP request to [[S3]].
- **Most recently used data is cached in file gateway**, so it doesnt have to be fetched from AWS.
- Transation into Glacier using a Lifecycle Policy.
- IAM Roles for each FG.

![[st_gateway_s3.png]]

### Volume Gateway

- Block Storage using iSCSI protol backed by S3.
- Backed by [[EBS]] snapshots.
- **Cached volumes**: low latency access to most recent data.
- **Stored volumes**: entire dataset is on-premise, scheduled backups to S3.

### Tape Gateway

- Uses Virtual Tape libray.
- For backup processes using physical Tapes.
- Can send directly into [[S3]] Glacier.

### FSx File Gateway (discontinued, won't appear on the exam)

- Native access to [[FSx]] for Windows File Server.
- Local cache for frequently accessed data.
- Windows native compatiblity (SMB, NTFS, AD).
- Group file shares and home directories.

## Hardware appliance

- Using Storage Gateway means you need on-premises virtualization.
- Otherwise, you can use **Storage Gateway Hardware Appliance**.
- Can be bought from amazon.com.
- Is a harware which will be your gateway (like a firewall).
