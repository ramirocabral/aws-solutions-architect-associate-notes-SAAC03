![[Pasted image 20221101163353.png]]

## TLDR
Message queue with a subscriber model. It can send the same message to alot of diffrent services at once. Scales good but not indefinetly. Pub/Sub.

## Features

- Subscriber async model.
- One producer multiple consumers/subscribers.
- Each subscriber to the topic will get all the messages.
- Up to 12 million subscribtions per topic.
- Up to 100k topics.

## Sources

- [[CloudWatch]] alarms.
- [[ASG]] Notifications.
- AWS Budgets [[AWSBilling]].
- [[Lambda]].
- [[DynamoDB]].
- Cloudformation.
- ....

## Targets

- [[Kinesis]] Data Firehouse.
- [[SQS]].
- [[Lambda]].
- HTTP.
- E-Mail.
- Push.
- Sms.

## Publish

- **Topic Publish** (with SDK).
  - Create a topic.
  - Create one or more subscribers.
  - Publish to the topic.
- **Direct Publish** (mobile apps SDK)
  - Create a platform app.
  - Create a platform endpoint.
  - Publish to the platform endpoints.

## Security

- HTTPS by default.
- At rest using [[KMS]] keys.
- Client side optional.
- IAM for access control.
- **SNS Access Policies**, resource based for cross account or other services.

## SNS + SQS: Fan Out

- Push once in SNS, receive in all SQS queues that are subscribers.
- Fully decoupled, no data loss.
- SQS allows for: data persistence, delayes processing and retries of work.
- Ability to add more queues over time.
- SQS queue access polycy must allow SNS to write.

![[fan_out.png]]

## FIFO Topic

- Ordering of messages in the Topic.
- Same features as FIFO SQS queues.
- Can have SQS Standard and FIFO queues as subscribers.
- Limited throughput.

## Message Filtering

- JSON policy to filter messages sent to SNS subscribers.
- If a subscription doesn't have a filter policy, it receives all messages.
