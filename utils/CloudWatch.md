![[Pasted image 20221101162633.png]]

## Features
- Provides metrics for **every** service in AWS

## Metrics
- A variable to monitor (CPU, Network, etc).
- Metrics belong to **namespaces**.
- Matrics have timestamps.
- Can create custom metrics.
- Can stop, terminate, reboot and recover [[EC2]] instances.
- Can trigger [[Lambda]] or [[EventBridge]].

### CloudWatch Metrics Streams

- Continually stream cloudwatch metrics to: (near-real-time)
  - [[Kinesis]] Firehouse.
  - 3rd party providers.
- Option to **filter metrics**.

## CloudWatch Logs

- **Log groups** (application name).
- **log stream**: instance within application / log files / containers.
- Log expiration policies.

### Targets To Send Logs To

- [[S3]].
  - Up to 12 hours.
  - API call : `CreateExportTask`.
  - Not real-time or near-real-time.
- With **Logs Subscriptions**, filter with **Susbcription Filters** and send to:
  - [[Kinesis]] data streams.
  - [[DataFirehose]].
  - [[Lambda]].
  - [[OpenSearch]].
- **Cross-Account Subscriptions**.

### Logs sources

- SDK.
- CloudWatch Logs Agent.
- CloudWatch Unified Agent.
- [[ElasticBeanstalk]], collection of logs from applciation.
- [[ECS]],collection from containers.
- [[Lambda]], collection from function logs.
- [[VPC]], flow logs.
- [[APIGateway]].
- [[CloudTrail]], based on filter.
- [[Route53]], DNS requests.

### Logs Insights

- Search and analyze log data stored in CloudWatch Logs.
- Purpose-built query language.

## CloudWatch Agent

- Allows to collect logs from [[EC2]] instances.
- Run a CloudWatch agent on EC2 to push the log files.
- Need correct IAM Role.
- Can be setup on-premises too.

### Logs Agent and Unified Agent

- For virtual servers.
- **Logs Agent**.
  - Old version.
  - Can only send to CloudWatch Logs.
- **Unified Agent**.
  - Collect additional system-level metrics:
    - **CPU**.
    - **Disk metrics**.
    - **RAM**.
    - **Netstat**.
    - **Processes**.
    - **Swap Space**.
  - Collect logs to send to CloudWatch Logs.
  - Centralized config using [[SSM]] Parameter Store.

## CloudWatch Alarms

- Trigger notifications for any metrics.
- States:
  - OK.
  - INSUFFICIENT_DATA.
  - ALARM.
- Period: length of time to evaluate the metric.
- Can be created based on **CloudWatch Logs Metric filters**.
- To test, can set the alarm state using CLI.

![[cloudwatch_logs_alarms.png]]

### Targets

- [[EC2]] instances: stop, terminate, reboot, recober.
- [[ASG]]: Trigger auto-scaling action.
- Send notification to [[SNS]].

### Composite Alarms

- Composite alarms monitor the states of multiple other alarms.
- AND or OR conditions.
- Helpful to reduce "alarm noise".

## [[EC2]] Instance Recovery

- **Status check**:
  - Instance status: check the EC2 VM.
  - System status: check the underlying hardware.
  - Attached EBS status: check EBS volumes.
- **Recovery**: same private, public, elasticIP, metadata, placement group.

## Insights

### Container Insights

- Collect, aggregate and summarize **metrics and logs** from containers.
- From:
  - [[ECS]].
  - [[EKS]].
  - Self-managed Kubernetes in EC2.
  - Fargate.
- In EKS and Kubernetes, uses a containerized version of the CloudWatch agent.

### Lambda Insights

- Collects, aggreagates and summarizes system-level metircs, including CPU time, memory, disk and network. Also, info about cold starts and worker shutdowns.
- Provided as a Lambda Layer.

### Contributor Insights

- Analyze log data and create time series that display contributor data.
- Helps finding top talkers and understand who or what is impacting system performance. **Top-N contributors**.
- Works for any AWS-generated logs.
- For example, identify heaviest network users, or find URLS that generate the most errors.
- Built-in rules to analyze metrics from other AWS services.

### Application Insights

- **Automated** dashboards that show potential problems with monitored applications.
- Help isolate ongoing issues.
- Powered by Sagemaker ([[ML]]).
- Enhanced visibility for app health. Reduce the time it will take to troubleshoot and repair applications.
- Findings and alerts are sent to [[EventBridge]] and [[SSM]] OpsCenter.
