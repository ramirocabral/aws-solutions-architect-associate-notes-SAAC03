![[Pasted image 20221101171725.png]]

# Web Application Firewall

- Protection against L7 exploits (http).

## Deploy Targets

- ALB [[ELB]].
- [[APIGateway]].
- [[CloudFront]].
- AppSync GraphQL API.
- [[Cognito]] User Pool.

## Web ACL Rules

- **IP Set**: up to 10k addresses. Use multiple rules for more IPS.
- HTTP header, body, or URI strings. **SQL injection and XSS**.
- Size constraints, **geo-match (block countries)**.
- **Rate-based rules** (to count occurrennces of events) **DDoS protection**.
- Web ACLs are Regional except for [[CloudFront]].
- Rule group -> reusable set of rules that you can add to a web ACL.
