# Secrets Manager

- vs SSM newer, force rotation every x days, automate generation of keys.
- Secrets can be encrypted using [[KMS]].
- To rotate keys, you can use a custom Lambda function.
- Integration with [[RDS]], [[Aurora]], etc.

## Multi Region Secrets

- Replicate secret accros regions.
- Creates replica secrets.
- Keeps replicas in sync with the primary secret.
- Ability to promote a read reaplice Secret to a standalone secret.
- Can promote replica secrets to master.
- Used for disatery recovery of rds, multi-region db, etc.
