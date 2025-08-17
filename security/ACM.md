# AWS Certificate Manager

## Overview 

- Manage, provision and deploy SSL Certs.
- Supports putlic and private certs. (free of charge for public certs)
- Automatic cert renewal.
- Can use it with [[ELB]], [[CloudFront]] districutions, [[APIGateway]].
- Cannot use them with [[EC2]] directly.

## Requesting Public Certificates

1. List domain names to be included in the cert.
2. Select DNS or Email validation.
3. Wait a few hours.
4. The Public Certificate will be enrolled for automatic renewal. (60 days before expiration)

## Importing Public Certificates

- **No automatic renewal**.
- ACM sends daily expiration events 45 days prior to expiration in [[EventBridge]].
- [[Config]] has a managed rule named `acm-certificate-expiration-check` that checks for expiring certs.

## Integration with API Gateway

- Create a **Custom Domain Name** in API Gateway.
- **Edge-optimized endpoints**.
  - The TLS cert must be in the same region as CloudFront (us-east-1).
  - Then setup CNAME or Alias record in Route53.
- **Regional endpoints**.
  - The TLS cert must be imported on API Gateway, in the same region as the API Stage.

## IAM certificate Store

- Used for regions where ACM is not available.
- Can be used via CLI.
