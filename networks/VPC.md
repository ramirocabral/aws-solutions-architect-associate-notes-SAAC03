![[Pasted image 20221101210003.png]]

## TLDR

A stack of AWS resources, more clearly the connectivity and setup options for and between these resources.

## Overview

- Max 5 VPCs per region (soft limit).
- Max CIDR per VPC is 5, for each CIDR:
  - Min size is /28 (16 IPs).
  - Max size is /16 (65,536 IPs).
- Only private IPv4 ranges are allowed:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16
- **Your VPC CIDR should NOT overlap with your other networks.**

## Subnets

- A VPC can have multiple subnets.
- AWS reserves **5 IP addresses** (first 4 and last one) in each subnet.

## Internet Gateway (IGW)

- Allows resources in a VPC to connect to the internet.
- Must be created separately from a VPC.
- One VPC can only be attached to one IGW and vice versa.
- On their own do not allow internet access, need to be used with a route table.
- **It does not NAT by default**. So without nat, resources in a public subnet need to have public IP addresses to access the internet.

### Egress-only IGW

- For IPv6 only.
- Similar to NAT Gatewat but or IPv6. Useful because all IPv6 addresses are public.
- Allows outbound connections while preventing inbound connections initiated by the internet.
- **Must update route tables**.

## Bastion Hosts

- EC2 instance in a public subnet.
- Used to access through SSH to resources in private subnets.
- **The security group must allow inbound from the internet on port 22 from restricted CIDR, for example the public CIDR of your office.**
- **The security group of the instances must allow the Security Group of the Bastion Host, or the private IP of the Bastion Host.**

<img src="attachments/vpc_bastion_hosts.png" width="350"/>

## NAT Instance (outdated)

- Allows EC2 instances in private subnets to connect to the internet.
- Must be launched in a public subnet.
- Must disable EC2 setting: source/destination check. 
- Must disable Elastic IP attached to it. (the ip may change in the middle of a connection)
- Route tables must be configured to route traffic from private subnets to the NAT instance.
- Pre-configured Amazon Linux AMI with NAT enabled is available.
- Not highly available.
- Can be used also as bastion host.

<img src="attachments/nat_instances.png" width="350"/>

## NAT Gateway (NATGW)

- AWS managed NAT, higher bandwith, high availability.
- Pay per hour for usage and bandwidth.
- Created in a specific AZ, uses an Elastic IP.
- Can't be used by EC2 instances in the same subnet.
- Required an IGW.
- 5Gbps with automatic scaling to 100Gbps.
- No SGs required.
- Must create **multiple NATGWs** in **multiple AZs** for fault-tolerance.

## NACLs

- Like a firewall, control traffic from and to **subnets**.
- NACLs are **stateless**, Security Groups are **stateful**.
- **One NACL per subnet**, new subnets are associated with the default NACL.
- **NACLS Rules:**
  - Number (1-23766), high precedence with a lower number. First rule match will drive the decision.
  - Last rule is an asterisk (*), denies a request in case of no rule match.
  - AWS recommends adding rules by increment of 100.
- Newly created NACLs are **DENY ALL** by default.
- Great way for blocking a specific IP at the subnet level.

### Default NACL

- Accepts everything in/out.

## VPC Peering

- Privately connect two VPCs using AWS' network.
- Make them behave as if they were in the same network.
- **NOT transitive**, meaning if VPC A is peered with VPC B, and VPC B is peered with VPC C, A cannot access C.
- Must update route tables **in each VPC's subnets** to ensure EC2 instances can communicate with each other.
- Can be cross-account and cross-region.
- Can reference a security group in a peered VPC.
- CIDR blocks must not overlap.

## VPC Endpoints

- Allows to connect to AWS services using a **private networ** instead of using the public internet.
- Redundant and scalable.
- No need for IGW, NAT, VPN or Direct Connect.

<img src="attachments/vpc_endpoints.png" width="400"/>

### Interface Endpoints

- Powered by AWS PrivateLink.
- Provisions an ENI (private IP) as an entry point (must attach a SG).
- Supports most AWS services.
- $ per hour + $ per GB processed.
- Preferred for acess from on-premises, a different VPC or a different region.

### Gateway Endpoints

- Provisions a gateway and must be used as a target in a route table. (does not uses SGs)
- Supports S3 and DynamoDB.
- Free.
- **Most likely the preferred solution on the exam**.

## VPC Flow Logs

- Capture information about IP traffic going into your interfaces:
  - VPC Flow Logs.
  - Subnet Flow Logs.
  - ENI Flow Logs.
- Data can go to [[S3]], [[CloudWatch]] Logs, or [[DataFirehose]].
- Captures network information from AWS managed interfaces too: [[ELB]], [[RDS]], [[ElastiCache]], [[Redshift]], NATGW, etc.
- Can be queried using [[Athena]] on [[S3]] or [[CloudWatch ]] Logs Insights.
 
<img src="attachments/vpc_flow_logs_syntax.png" width="800"/>

## Site-to-Site VPN

- Connects your on-premises network to an AWS VPC.
- **Virtual Private Gateway** (VGW).
  - AWS side of the VPN connection.
  - Created and attached to the VPC from which you want to create the Site-to-Site VPN connection.
  - Must enable **Route Propagation** for the VGW in the route table associated with the subnetCustomer connections can connect to each other.s
  - Can customize the ASN (Autonomous System Number) for BGP.
- **Customer Gateway** (CGW).
  - Software or physical device on customer side.
  - Must have a internet-routable IP address.
  - If it's behind a NAT that's enabled for NAT traversal, use the public IP address of the NAT device.

### VPN CloudHub

- Provide secure communication between multiple sites, when having multiple VPN connections.
- Hub-and-spoke model for primary or secondary network connectivity between different locations.
- Customer connections can connect to each other.
- To set it up: connect multiple VPN on the same VGW, setup dynamic routing and configure route tables.

<img src="attachments/vpc_cloudhub.png" width="500"/>

## DirectConnect (DX)

- **Dedicated private connection** from a remote network to your VPC.
- Need to setup a VGW on your VPC.

<img src="attachments/vpc_dx.png" width="700"/>

### Connection Types

- **Dedicated Connection**: 1Gbps, 10Gbps and 100Gbps.
  - Physical ethernet port dedicated to a customer.
  - Request to AWS and completed by AWS Direct Connect Partners.
- **Hosted Connection**: 50Mbps, 500Mbps, to 10Gbps
  - Connection requests via AWS Direct Connect Partners.
  - Capacity can be **added or removed on demand**.

**1 month to establish a new connection!**

### Encryption

- Data in transit is **not encrypted**, but the connection is private.
- Must setup a IPsec VPN to encrypt the traffic.

### Resiliency

- **High resiliency**: One connection at multiple locations.
- **Maximum resiliency**: Separate connections terminating on separate devices in more than one location.

In case DX fails, you can set up a Site-to-Site VPN as a backup.

### Use cases

- Increase bandwidth throughput.
- More consistent network experience.
- Hybrid environments.

### Direct Connect Gateway

- Setup a DX to one or more VPC in many different regions. (same account)

<img src="attachments/vpc_dx_gateway.png" width="700"/>

## Transit Gateway (TGW)

- For having **transitive peering between thousands of VPC and on-premises**, hub-and-spoke connection.
- Regional resource, can work cross-region.
- Share cross-account using RAM (Resource Access Manager). Can be used to share a DX connection with multiple accounts.
- Route tables: limit which VPC can talk with other VPC.
- Supports Multicast.
- Can increase bandwidth to AWS using ECMP.

<img src="attachments/tgw.png" width="350"/>

## Traffic Mirroring

- Capture and inspect network traffic in your VPC.
- Route the traffic to security applicances that you manage.
- Capture all traffic or only specific traffic.
- Source and target can be in the same VPc or different VPCs. (VPC peering)
- Capture the traffic:
  - From ENI
  - To ENI or NLB.

## IPv6 in VPC

- IPv4 cannot be disabled.
- IPv6 can be enabled to operate in dual-stack mode.
- Your EC2 instances will get at least a private internal IPv4 and a public IPv6.
