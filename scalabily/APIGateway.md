![[apigateway.png]]

## Overview

- Lambda + API Gateway = No infra to manage.
- Supports WebSockets.
- Handle API versioning.
- Handle different environments, security.
- Create API keys, handle request throttling.
- Swagger/OpenAPI to quickly define APIs.
- Cache API responses.

## Integrations

- **[[Lambda]] Function**
  - Invoke Lambdas.
  - Expose REST APIs backed by Lambda.
- **HTTP**
  - Expose HTTP endpoints in the backend.
  - Example: internal HTTP API on premise.
- **AWS Service**
  - Expose any AWS service as an API.

## Endpoint Types

### Edge Optimized (default)
- Routed through [[CloudFront]] Edge Locations.
- The API Gateway still lives in only one region.
- For global clients.

### Regional
- Clients within the same region.
- Manually combine with [[CloudFront]] for more control.

### Private
- Only from within your [[VPC]].
- Can use Resource policy.

## Authentication

- [[IAM]] Roles (for internal Application).
- [[Cognito]] for External Users.
- Custom Authorized (using [[Lambda]] and own code).

### Custom Domanin name HTTPS

- Use [[ACM]].
- If running Edge-Optimized endpoint, then the certificate must be in us-east-1.
- If using Regional Endpoint, the certificate must be in the API Gateway Region.
- Must setup CNAME or A-alias record in [[Route53]].
