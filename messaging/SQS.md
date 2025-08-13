![[sqs.png]]

## TLDR

AWS standard queue service. Has ton of features like fifo and multi consumer. Scales indefinetly.

## Features
- **Decouple applications**.
- Unlimited throughput.
- Default retention: 4 days, maximum of 14 days.
- Low latency.
- Message size <= 256 KB.
- Can have duplicate messages. (at least once delivery)
- Can have out of order messages. (best effort ordering)

## Producing Messages

- Produced using the SDK. (SendMessage API)
- Message is **persisted** until a consumer deletes it.

## Consuming Messages

- Running on EC2 instances, on-premise, Lambda, etc..
- Poll for messages. (receive up to 10 messages at a time).
- Process the messages.
- Delete the messages using the DeleteMessage API.

## Common Patterns

### SQS with ASG

- CloudWatch Metric -> Queue Length.
- We can set an alarm on the queue length to scale out/in the ASG.

![[sqs_asg.png]]

### SQS as a buffer to database writes

![[sqs_buffer.png]]

## Security

### Encryption

- In-flight encryption using HTTPS API.
- At-rest encryption using KMS keys.
- Client-side encryption available.

### Access Control

IAM policies to regulate access to the SQS API.

### SQS Access Policies (similar to S3 bucket policies)

Useful for cross-account access to SQS queues.

## Message Visibiliity Timeout

- After a message is polled by a consumer, it becomes **invisible** to other consumers.
- By default, "message visibility timeout" = 30 seconds.
- So, the message has 30 seconds to be processed.
- After that time, the message becomes visible again.
- If a consumer needs more time, it can extend the visibility timeout using the ChangeMessageVisibility API.
- Visibility Timeout high -> if failure, re-processing will take time.
- Visibility Timeout too low -> we may get duplicates.

## Long Polling

- After requesting a message, a consumer can "wait" for messages to arrive if the queue es empty.
- Decreases API calls, increases the efficiency and reduces the latency
- Between 1 and 20 sec.
- WaitTimeSeconds API.

## FIFO Queues.

- Message ordering.
- Limited throughput: 300 msg/s without batching, 3000 msg/s with batching.
- Exactly-once send capability. (with Deduplication ID).



