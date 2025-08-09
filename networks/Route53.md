![[Pasted image 20221101114116.png]]

AWS Nameserver and Domain Name register Service.

## Features

- Highly available, scalable, fully managed and Authoritative DNS service.
- Domain Registar (can register own names).
- 100% availabilty.
- Health checks.

## DNS Record

Each record contains:

- **Domain/subdomain name**: e.g. example.com, test.example.com.
- **Record type**: A, AAAA, CNAME, etc.
- **Value**: e.g. 1.2.3.4.
- **Routing Policy**: how Route 53 responds to DNS queries.
- **TTL**. Mandatory to every record except Alias records.

### Record types supported

- **A** : hostname -> IPv4.
- **AA**: hostname -> IPv6.
- **CNAME**: maps DNS querys to another hostname.
- **NS**: Name Servers for the Hosted Zone.

#### CNAME vs Alias Records

- **CNAME**: can map a hostname to another hostname. ONLY FOR NOT ROOT DOMAIN
- **Alias**: Points a hostname to an AWS resource. (app.mydomain.com -> myservice.amazonaws.com). CAN BE USED FOR ROOT DOMAIN.
  - Free of charge.
  - Native health check.
  - Is always of type A/AAA for AWS resources.
  - Can't set the TTL.
  - Cannot point to an EC2 DNS name.

## Hosted Zones

Container for records that define how to route traffic to a domain and its subdomains.

- **Public Hosted Zones**: containes records that specify how to tourte traffic on the Internet.
- **Private Hosted Zones**: contain records that specify how you route traffic within one or more VPCs. (private domain names)

- $0.50 per month per hosted zone.

## Routing Policies

- Simple.
- Weighted.
- Failover.
- Latency-based.
- Geolocation.
- Multi-value answer.
- Geoproximity (traffic flow only).
- IP-based routing.

## Health Checks

- Only for public resources.
- For automated DNS failover.
- They can monitor:
  1. An endpoint (app, server, other AWS resource).
    - 15 global checkers will check the health.
    - > 18% of healthcheckers detect it healthy -> endpoint healthy, else unhealthy.
  2. Other health checks. (Calculated health checks).
    - Combine the results of multiple health checks. Can use OR, AND, NOT.
  3. CloudWatch alarms. (helpful for private resources).
- Integrated with Cloudwatch Alarms.

For Private Hosted Zones, you can use Cloudwatch Alarms and use it to check the health of the resources.

<img src="attachments/route53_health_checks.png" width="400"/>

### Simple Policy

- Route traffic to a single resource.
- Can specify multiple values in the same record. A random one is chosen by the client.
- Can't be associated with health checks.

### Weighted Policy

- Control the % of the requests that go to different resources.
- DNS records must have the same name and type.
- Can be associated with health checks.

### Latency-based Policy

- Redirect to the resource that has the least latency to us.
- Latency is based on traffic between users and AWS Regions.
- Can be associated with health checks.

### Failover Policy (Active-Passive)

- We have a primary resource and a secondary resource.
- We need a health check to determine if the primary resource is healthy.
- Primary resource healthy -> traffic is routed to it.
- Primary resource unhealthy -> traffic is routed to the secondary resource.
- The secondary resource can have an optional health check.

### Geolocation Policy

- The routing is based on user location.
- Should create a "default" record. (when there's no match on location)
- Use case: website localization, restrict content distribution, etc.
- Can be associated with health checks.

### Geoproximity Policy (Traffic Flow only)

- Route traffic to your resources based on the geographic location of users and resouces.
- **Shift more traffic to resourcesd** based on the defined bias.
- To change the size of the geographic region, specify bias values.
- Can be AWS resouces or external resources (specify Lat and Long).

![[route53_geoproximity_policy.png]]

### IP-Based Routing Policy

- Routing is based on client's IP addresses.
- CIDR -> endpoints/locations.
- Use cases: optimize performance, reduce network costs, route ISP users...

### Multi-Value Answer Policy

- Routing traffic to multiple resources.
- Returns multiple values/resources.
- Can be associated with health checks.
- Up to 8 healthy records.
- Client-Side Load Balancing.

## Hybrid DNS

- Resolve DNS queries between VPC (Route 53 Resolver) and your networks (other DNS resolvers).

- Networks can be:
  - VPC/Peered VPC.
  - On-premises Network (connected with DirectConnect or AWS VPN).

### Resolver Endpoints

- **Inbound**: DNS resolvers on your network can forward DNS queries to Route 53 Resolver. Allows your Resolvers to resolve domain names of AWS resouces and records in Route 54 Private Hosted Zones.
<img src="attachments/route53_inbound_endpoints.png" width="700"/>
- **Outbound**: conditionally forwards DNS queries to your DNS resolvers. Uses **Resolver Rules**.
<img src="attachments/route53_outbound_endpoints.png" width="700"/>

- Associated with one or more VPCs in the same region.
- Create in two AZs for high availability.

### Resolver Rules

- **Conditional Forwarding Rules**
  - Forward DNS queries for a specified domain and all its subdomains to target IP addresses.
- **System Rules**
  - Overried Forwarding rules.
- **Auto-defined System Rules** (internal resolving)
  - Defines how DNS queries for selected domains are resolved.

Route 53 Resolver chooses the most speficic match.

Resolver Rules can be shared across accounts using AWS RAM.
