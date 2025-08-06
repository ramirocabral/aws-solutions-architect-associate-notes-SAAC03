![[Pasted image 20221101204757.png]]
# EBS (Elastic Block Store)

**Network Drive** that can be attached to [[EC2]] instances.

## Features

- Network Drive (might have some latency).
- Persist Data after termination.
- Bound to a specific [[AZ]].
- Can be mounted to multiple instances in the same AZ. (**multi-attach**).
- Attached and detached quickly.
- Snapshot needed to change AZ.
- Provisioned capacity (Size and IOPS).
- You get billed even if drive is not full.
- **Delete on termination** --> volume deleted when instance is terminated.(default ON).
- Can be modified while in use (IOPS and capacity).

## EBS Snapshots

- Backup of an EBS volume.
- Can be copied to different AZ/Region.
- Can be done while the volume is being used (NOT RECOMMENDED).

**EBS Snapshot Archive**: Cheaper Snapshot storage but longer restore time (24h-72h).

**EBS Recycle Bin** : Can enable recycle for recovery (retention 1 day TO 1 year). Can be used for IAM images and EBS Snapshots.

**Fast Snapshot Restore (FSR)**: No latency on restore, but costs more.

## Volume types

EBS volumes are characterized by Size, Throughput and IOPS.

- **GP2/GP3**: General purpose SSD, cost effective, low latency.
- **IO1/IO2**: Highest-Performance SSD. Mission critical, low latency. Supported for Multi-Attach.
- **ST1 (HDD)**: Low cost HDD, throughput intensive workloads.
- **SC1 (HDD)**: Lowest cost HDD, less frequently accessed workloads.

**Only SSD volumes can be used as boot volumes.**

## EBS Multi attach

- Same AZ can attach same volume to multiple instances.
- Only available for io2 and io1.
- Each instance has full R/W permissions.
- Cluster linux applications, concurrent write operations.
- Max of 16 [[EC2]] instances.
- FS must be cluster aware.

## EBS Encryption

- Data at rest is encrypted.
- Snapshots are encrypted and all the volumes created from it.
- Data is encrypted in flight between [[EC2]] instances and the volume.
- Handled transparently.
- Minimal impact of latency.
- Uses keys from [[KMS]] (AES-256).
- Copying and unencrypted snapshot enables encryption.
- Unencrypted volumes -> Unencrypted snapshots.

### Encrypt volume currently not encrypted

- Create Snaphsot.
- Encrypt snapshot.
- Create new volume from snapshot.
- Attach new volume to original instance.
