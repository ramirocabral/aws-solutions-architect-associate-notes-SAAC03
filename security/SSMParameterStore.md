# Systems Manager Parameter Store

- Secure storage for configuration and secrets. ex: db password, api keys, etc.
- Optional encryption using [[KMS]].
- Serverless, scalable, easy SDK.
- Version tracking of configs/secrets.
- Security through [[IAM]].
- Notifications with [[EventBridge]].

## Path

- prod/db/pw e.g.

## Tiers

### Standard

- Up to 10k parameters.
- Max size KB.
- No policies.
- No additional charge.
- No storage pricing.

### Advanced

- Storage up to 100k
- Max size KB
- Policies can be used.
- 0.05 cent per parameter per month.
- Thoughput the same as standard.

## Parameters Policies

- Assign a TTL to a parameter.
- Can assign multiple policies at a time.
- Notifications through [[EventBridge]].
