![[Pasted image 20221101164642.png]]
# Elasticache

Managed Redis and Memcached service by AWS.

## Features
- In memory data store.
- Boost performance of DBs.
- Helps making applications stateless.
- Involves app changes.

## Use Cases
- Read heavy hpc tasks.
- Compute heavy hpc tasks.
- Session stores.
- High performance db caching.
- ...

## Redis

- **Multi AZ** with Auto-Failover.
- **Read replicas** to scale reads and have **high availability**.
- Data Durability using AOF persistence.
- Backup and restore features.
- Supports Sets and Sorted Sets.

## Memcached

- Sharding.
- No high availability (replication).
- Non persistent.
- Backup and restore.(serverless)
- Multi-threaded.

## Security
- no [[IAM]] Auth
- can us ssl encruption for in flight

## Loading patterns
- lazy (all read data is cached, but can become stale)
- write through (adds or updates to the db are mirrored in the cache)
- session store (expire data with time to live)

## Cache Security

- Support for IAM Authentication only for Redis.
- **Redis AUTH**: password authentication. Extra level of security. SSL encryption.
- Memcached supports SASL authentication.

## Patterns for using ElastiCache

- **Lazy Loading**: all the read data is cached, but can become stale.
- **Write Through**: adds or updates data in the cache when written to a DB.
- **Session Store**: expire data with TTL.

## Redis Use Case

- Gaming Leaderboards.
- **Redis Sorted Sets** guarantee both uniqueness and order.
