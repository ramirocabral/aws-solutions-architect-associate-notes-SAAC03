![[Pasted image 20221030232727.png]]

## TLDR

Developer centric view of deploying an application. uses EC2, ASG, ELB, RDS, etc.

## Features

- Automatically handles provisioning, load balancing, scaling, application health monitoring, etc. (PaaS)
- Only the application code is the respoinsibility of the developer.
- Fee, only pay for the underlying resources.
- Supports Docker.
- Single instance -> dev.
- High availability -> prod.

## Components

- **Application**: collection of Beanstalk components. (environments, versions, configurations...).
- **Application version**: an iteration of your application code.
- **Environment**:
  - Collection of AWS resources running an application version.
  - **Tiers:** Web Server Environment Tier & Worker Environment Tier (uses SQS queue, scale based on the \#messages).

<img src="attachments/beanstalk_iteration.png" width="600">
