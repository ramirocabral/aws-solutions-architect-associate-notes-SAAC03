![[cloudtrail.png]]

## Overview

- Provides governance, compliance and audit for AWS accounts.
- Enabled by default.
- Tracks and logs API requests within the aws account.
- Can put logs on [[CloudWatch]] Logs or [[S3]].
- A trail can be applied to all regions or a single region.
- Resource deleted -> Investigate CloudTrail first!

## CloudTrail Features

- **Management Events**:
  - Operations that are performed on resources in your AWS account.
  - **By default, trails are configured to log management events**.
  - **Read events** (don't modify resources) and **Write Events** (may modify resources).
- **Data Events**:
  - **By default, not logged**.(becuase of high volume)
  - Amazon S3 object-level activity.
  - [[Lambda]] function execution activity.
- **CloudTrail Insights Events**:
  - **Detect unusual activity** in your account.
  - Analyzes normal management events to create a baseline.
  - Continuosly analyzes write events to detect unusual patterns.
  - Events are sent to S3.
  - An EventBridge event is generated.

## Events Retention

- Events are stored for 90 days in CloudTrail.
- To keep them for longer, can send them to [[S3]] and use [[Athena]] to analyze them.
