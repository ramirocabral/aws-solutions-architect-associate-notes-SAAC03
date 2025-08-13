![[Pasted image 20221030232125.png]]

## TLDR

Kubernetes in AWS. [[ECS]] Default options are not Kubernetes, but AWS own tech.

## Features

- Supports [[EC2]] and [[Fargate]].

## Options

### Manged Node Groups

- Creates [[EC2]] instances for you.
- [[ASG]] managed by EKS.
- Nodes are part of an [[ASG]] managed by EKS.
- Supports on demand and spot instances.

### Self Managed Nodes

- [[EC2]] created by the user and registered to the cluster.
- Can use prebuilt [[EKS]] optimized [[AMI]].
- Supports on-demand or spot instaces.

### Fargate

- No nodes, instances or maintance required

## Data volumes

- Need to specify storage class.
- levarages a Container Storage Interface (CSI) driver to manage volumes.
- [[EBS]].
- [[FSx]] for Lustre.
- [[FSx]] for NetApp ONETAP.
- [[EFS]] (works with fargate).
