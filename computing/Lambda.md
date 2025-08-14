![[Pasted image 20221030233208.png]]
# AWS Lambda

## TLDR

With AWS Lambda you dont care about any infrastructure, you just upload a function to aws. You can than use that function from other services like  [[APIGateway]], [[SNS]] or even [[CLI]]. You upload Lambda code as a zip.

## Features

- Run code serverless.
- Pay per compute time.
- Scaling is automated.
- No charge if not running.
- Operates from AWS owned[[VPC]].
- You can enable function [[VPC]] access if you need private resources from your [[VPC]].
- Scale up based on request amount.
- Increasing RAM will also improve CPU and network.
- Can be packaged and deployed as container images.

## (some) Integrations

- [[APIGateway]]
- [[Kinesis]]
- [[S3]]
- [[CloudFront]]
- [[DynamoDB]]
- [[SNS]]
- [[SQS]]
- [[Cognito]]
- [[EventBridge]]

## Pricing

- Pay per calls: 
  - $0.20 per 1 million requests. (first million free)
- Pay per duration: 
  - 400,000 GB-seconds of compute time per month free. (400,000 seconds if function is 1GB RAM)
  - After, $1.00 for 600,000 GB-seconds.

## Limits (per region)

- **Execution**:
  - Memory allocation: 128MB to 10GB (1 MB increments).
  - Maximum execution time: 15 minutes.
  - Env variables (4 KB).
  - Disk capacity (/tmp): 512MB to 10GB.
  - Concurrent executions: 1000 (can be increased).
- **Deployment**:
  - Max zip size: 50MB.
  - Size of uncompressed deployment: 250MB.
  - Size of env variables: 4KB.

## Concurrency and Throttling

 - Can set a **"reserved concurrency"** at the function level.
 - Limits the function to not scale beyond the limit.
 - Each invocation over the limit will trigger a "Throttle".
 - Throttle behavior:
   - If **synchronous invocation** -> return ThrottleError-429.
   - If **asynchronous invocation** -> retry automatically and then go to DLQ.(send to the event queue and attemps to run the function again for up to 6 hours).

## Cold Starts and Provisioned Concurrency

- **Cold Start**:
  - New instance -> code is loaded and code outside the handler run (init.)
  - If the init is large, this process can take some time.
  - First request served by new instances had higher latency than the rest.
- **Provisioned Concurrency**:
  - Concurrency is allocated before the function is invoked. (in advance)
  - Cold start never happens.
  - Application Auto Scaling can manage concurrency.

## SnapStart

- Improves Lambdas performance up to 10x at no extra cost for Java, Python and .NET.
- When enabled, function is invoked from a pre-initialized state.
- When you publish a new version:
  - Lambda initializes your function.
  - Takes a snapshot of memory and disk state of the initialized function.
  - The snapshot is cached.

<img src="attachments/lambda_snapstart.png"  width="350" style="display: block; margin: auto;">

## Customization at The Edge

- **Edge Function**: Code attached to CloudFront distributions. Runs close to users to minimize latency.
- CloudFront provides two types: **CloudFront Functions** and **Lambda@Edge**.

<img src="attachments/cloudfront_functions.png"  width="200" style="display: block; margin: auto;">

### Use cases

- Website Security and Privacy
- Dynamic Web Application at the Edge.
- SEO.
- Intelligently Route Across Origins and Data Centers.
- Bot Mitigation.
- A/B testing.
- ...

### CloudFront Functions

- Lightweight JavaScript functions.
- For high-scale, latency-sensitive CDN customizations.
- Change Viewer Requests and responses.

### Lambda@Edge

- NodeJS or Python functions.
- Scales to **1000s of request/second**.
- Change Viewer/Origin Requests and responses.
- Author functions in one region (us-east-1), then CloudFront replicates to its locations.

## Lambda on VPC

By default, Lambda runs in an AWS-owned VPC. (cannot access resources in your VPC)

- You must define VPC ID, the Subnets and SGs.
- Lambda will create an ENI in your subnets.
