![[fsx.png]]

- Launch 3rd party high-performance file systems on AWS.
- Fully managed.
- Supports:
  - Lustre.
  - Windows File Server.
  - Netapp ONTAP.
  - OpenZFS

## For Windows File Server

- Supports SMB & Windows NTFS.
- Supports AD, ACLs, user quotas.
- **Can be mounted on Linux EC2 instances**.
- Can use **Microsoft DFS Namespaces** for group files across multiple FS.
- Storage options:
  - SSD.
  - HDD.
- Can be accesessed from on-premise with VPN or DirectConnect.
- Can be configured to be Multi-AZ.
- Data backed-up daily on S3.

## For Lustre

- Lustre -> Distributed FS, for large-scale computing.
- Machine learning, HPC.
- 100 GB/s.
- Storage options:
  - SSD
  - HDD.
- Can **"read S3"** as a FS.
- Can be used from on-premises servers (VPN or DirectConnect).

## For NetApp ONTAP

- Compatible with NFS, SMB, iSCSI.
- Move workloads on ONTAP or NAS to AWS.
- Storage automatically shrinks or grows.
- High OS compatibility.
- Snapshots, replication, low-cost, compression and data de-duplication.
- Point-in-time instantaneous cloning.

## For OpenZFS

- Compatible with NFS.
- Up to 1mill IOPS.
- Snapshots, compression and low-cost.
- Point-in-time instantaneous cloning.

## File System Deployment Options

- **Scratch File System**
  - Temporary storage
  - Data not replicated.
  - High burst.
- **Persistent File System**
  - Long-term.
  - Data replicated within same AZ.
  - Replaced failed files within minutes.
