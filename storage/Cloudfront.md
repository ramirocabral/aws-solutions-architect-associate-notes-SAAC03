- CDN. Improves read performance.
- Global.
- Regional edge caches.
- HTTP based requests.
- DDoS protection.
- TTL.

## Origins

- **S3**.
  - Secured using Origin Access Control (OAC).
  - Cloudfront can be upload point to S3.
- **VPC**
  - For apps hosted in VPC private subnets.
  - E.g ALB, NLB, EC2 intances.
- **Custom Origin**
  - S3 website.
  - Any HTTP backend.

## VPC origins

- Deliver content for apps hosted in VPC private subnets.
- Deliver traffic to **private**:
  - ALB.
  - NLB.
  - EC2 Instances.

**When using public resources -> Need to allow the Edge Locations IPs on the Security Groups**

## Geo Restirction

- Whitelist/Blacklist countries.
- Used for Copyright Laws.

## Pricing

- Cost of data out per Edge Location varies.
- You can reduce the number of Edge Locations for **cost reduction**.
- Three price classes:
  1. Price Class All: all regions, best performance.
  2. Price Class 200: most regions, exclude most expensive regions.
  2. Price Class 300: only the least expensive regions.

## Cache Invalidations

- Force an entire or partial cache refresh (bypass the TTL) by performing a **CloudFront Invalidaton**.
- Invalidate all files or a special path.
