![[Pasted image 20221031141128.png]]

## TLDR

Serverless machine learning-powered business intelligence service to create interactive dashboards.

## Overview

- Fast, automatically scalable, embeddable, per-session pricing.
- Integrated with [[RDS]], [[Aurora]], [[Athena]], [[Redshift]], [[S3]] and 3rd party sources and on-premise infra.
- **In-memory computation using SPICE** engine if data is imported into QuickSight.
- Enterprise edition: **Column-Level Security (CLS)**.
- Define users (standard versions).
- Define user groups (only enterprise).
- These users **dont** equal  [[IAM]] users.

## Dashboard

- Read only snapshot for the analysis which can be shared.
- Preserves the configuration of the analysis.
- You can share the analysis or dashboard with users or groups.
- To share a dashboard, you must publish the analysis.
