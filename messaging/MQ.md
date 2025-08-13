# Message Queue

- Managed service for RabbitMQ or ActiveMQ.
- Used for migration if you dont want to migrate app.
- Topic and queue feature (emulate [[SQS]] and [[SNS]]).
- Multi-AZ.

## High Availability

- We have Multi-AZ with one Active and one Standby broker.
- Needs EFS for storage.
