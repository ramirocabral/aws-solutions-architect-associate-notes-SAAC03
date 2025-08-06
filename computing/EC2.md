![[Pasted image 20221030223457.png]]
# Elastic Compute Cloud

## TLDR
EC2 is a the combination of a virtual machines and hardware capacity attached to that vm in AWS. It is one of the oldest services and well integrated into most other services.

## Virtual Machines (EC2)

### Configuration Options

- OS (Win, Linux, MacOs).
- CPU.
- RAM.
- Network attached storage ([[EBS]] & [[EFS]]).
- Hardware attached ([[InstanceStore]]).
- Network Card (Speed, Ip).
- Firewall ([[SecurityGroup]]).
- Bootstrap script (User Data).

### User Data

- Script that runs once on the first start of the instance.
- Runs using root privileges.

### Instance Types

![[instance_type_nomenclature.png]]

#### Classes

Some of the available classes are:

- **General Purpose**: Balance between, computing, memory and network speed.
- **Compute Optimized** : Compute-intensive tasks. E.g. high performance web servers, scientific modeling, dedicated gaming servers.
- **Memory optimized** : Workloads that process large data sets in memory. E.g. databases, cache, realt-time big data processing.
- **Storage Optimized** : High amount of Disk IOPs. E.g. Databases, distributed FS, data warehousing.

## Purcharsing Options

### On Demand

- Pay for what you use.
- Price by second (min 60s).
- Short term and un-interrupted workloads.

### Reserved Instances

- 1 Year OR 3 Years 
- Payment options: All upfront, Partial upfront, No upfront.
- Reserve specific instante attributes (type, region, tenancy, os).
- Scope reserve in zone and AZ.
- You can sell peer to peer in the **Reserved Instance Marketplace**. (NOT THE AMI/SAAS MARKETPLACE).

**Convertible Reserved Instance:**
- More expensive than default
- Can change instance type, os, region, tenancy.

### [[SavingsPlans]]

- Commit to a certain type of usage.
- 1 Year OR 3 Years.
- Up to same discount as default reserved instance
- Beyond commit is billed on demand price.
- Locked to instance FAMILY and REGION.
- Can change OS, tenancy, and instance size.
- Usage beyond the commit is billed On-Demand price.

### Spot Instances

- Cheapest.
- Can lose instance.
- Most Cost-Efficient type of instances.
- Define max price you are willing to pay, if you are overbid your instance is gone.
- Useful for workloads resilient to failure.

### Dedicated Hosts

- Most expensive.
- Rent a physical server, control placement of that server.
- On demand or Reserved.
- For companies for strong regulatory or compliance requirements.
- Can convert to a dedicated instance.

### Dedicated Instances

- No other customer will share the hardware used by you.
- Hardware may be shared with other instances in the same account.
- No control over instance placement (hardware might be moved).
- Can convert to dedicated host.

### Capacity Reservations

- Reserve a capacity in a AZ for duration (on demand instance).
- No time commitment.
- No billig discount.
- Combine with Saving plan and Reserved Instances for same AZ to save money.
- Charged on demand price if instance is not running.
- For short term uninterrupted workload in a specific AZ.

## Spot Instance Requests

- Define a **Max Spot Price** we are willing to pay.
- We have the instance while **current spot price < max spot price**, then AWS will **interrupt** it, and we have a 2 min grace period to **stop** or **terminate** the instance.
- If you terminate your instance but not the request the instance will be relaunched.
- If you cancel your request your instance will still be running.

![[spot_instance_request.png]]

### Spot Fleets

- Set of Spot instances + (optionally) On-Demand instances.
- It will try to meet the target capacity, with price constraints.
- Define possible **Launch Pools** (Instance Type, AZ, OS).
- Define a budget and target capacity.
- The Fleet stops launching instances when reaching capacity or max cost.

The **strategies** to allocate them are:

- **Lowest price**: launch the lowest price pool. (cost optimization).
- **Diversified**: distributed across all pools. (availability).
- **Capacity optimized**: pool with the optimal capacity for the number of instances.
- **Price Capacity Optimized**: pools with highest capacity available, the select the pool with lowest price. (RECOMMENDED)

## Placement Groups

Placement strategy for a group of EC2 instances.

### Cluster

- **Low-latency group in a single AZ.**
- AZ fails -> all instances fail.
- Great network performance.
- Low latency and big data jobs with deadline.

### Spread

- Spread instances across hardware.
- Multi AZ.
- Different hardware.
- Limited to 7 instances per AZ per placement group.
- Reduced risk of simultaneous failure.
- Used for critical apps and High Availability.

![[placement_group_spread.png]]

### Partition

- Spreads instances across multiple partitions (each in a single AZ).
- Multi AZ.
- Instances in a partition do not share racks with the instances in the other partitions.
- Up to 100s of instances.
- 7 partitions per AZ.
- Instances can access the partition metadata.

![[placement_group_partition.png]]

## Networking in EC2

By default, EC2 instances come with:

- 1 Private IP.
- 1 Public IP. ($0.005 per hour).

### Elastic Ip

- A static IP which can be attached to Elastic Network Interfaces and other services.
- You own it as long as you don't release it.
- You can mask a fail by keeping the IP but changing the instance.
- Up to 5 per account, can request more than 5 from AWS.


## ENI Elastic Network Interfaces
- Virtual Network Card
- Can be used not only for ec2
- Eth0 = primary ENI
- Primary private ip
- Can add multiple for multiple private ips
- Can attach elastic ip
- Can attach mac adress
- Can attach and detach from instance
- Bound by AZ
### EFA Elastic Fabric Adapter
- use to accelerate high performance computing by providing os bypacc hardware interface
- cannot be used for windows 

### ENA Elastic Network Adapter
- use for high performance networking capabilitiies
- slower than efa

## EC2 Hibernate
- Standby for EC2, ram is saved
- Faster startup
- Root [[EBS]] must be encrypted
- Used for breaks in very long running tasks or if an instances takes very long to startup
- Can last no longer than 60 days
- Must be enabled before launch

## EC2 Instance Recover
- Creates a new EC2 instance which is identical to the previous ec2
- recovers private and public ip, metadat, elastic ip, instandce id
- data in memory is lost

## Limits
- by default your account has a maximum limit for ec2 instances based on the total vcpu used, you can submit a request to increase that limit
