![[Pasted image 20221102200732.png]]

## TLDR

AWS Backup is a service to centraly manage and review your backup strategies.

## Features

- Central place to manage and automate backups across AWS Services.
- Cross-region backups.
- Cross-account backups.
- PITR (Point in time recoery) support.
- On-demand and scheduled backups.
- Tag-based backup policies.
- Can create backup policies known as **Backup Plans**.

## Supported

- [[EC2]] 
- [[EBS]]
- [[S3]]
- [[RDS]]
- [[FSx]]
- [[Aurora]]
- [[DynamoDB]]
- [[Neptune]]
- [[EFS]]
- [[StorageGateway]]
- ...

## Target

- Back ups in [[S3]].

## Vault Lock

- Enforce a WORM state.
- Backups cannot be deleted. (even the root cant)
