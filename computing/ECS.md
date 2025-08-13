![[Pasted image 20221030231124.png]]

## TLDR
ECS is AWS Docker Service. You can launch and modify containers as tasks in multiple ways depending on your application and scale.

## [[EC2]] Based

- Need to have a ECS Cluster composed by [[EC2]] instances as the host for your containers.
- You are billed for depending on the [[EC2]].
- The [[EC2]] Instance must be running the ECS agent.
- AWS takes care of starting/stopping containers.

## Fargate Based

- Serverless.
- You just create Task definitions.
- Billed for CPU and memory used.
- By default 20GB of free block storage.

## IAM Roles

- **EC2 Instance Profile** (EC2 Launch Type only).
  - Used by the ECS agent.
  - Make API calls to ECS service.
  - Send container logs to CloudWatch.
  - Pull image from ECR.
  - Reference sensitive data in Secrets Manager or SSM Parameter Store.
- **ECS Task Role**.
  - Allows each task to have a specific role.
  - Use different roles for the different services.
  - Task Role is defined in the **Task Definition**.

## Load Balancer Integrations

- **ALB** supported and works for most cases.
- **NLB** recommended for high throughput / high performance use cases.

## Data Volumes (EFS)

- Mount EFS FS systems onto ECS tasks.
- Works for EC2 and Fargate.
- Tasks running in any AZ will share the same data in the EFS FS.
- Fargate + EFS = Serverless.

## ECS Service Auto Scaling

- Not equal to [[EC2]] Auto Scaling.
- Automatically increase/decrease the desired number of ECS tasks.
- ECS Auto Scaling uses AWS Application Auto Scaling.
  - ECS Service Avg CPU Utilization.
  - ECS Service Avg Memory Utilization.
  - ALB Request Count per Target.
- **Target Tracking**: scale based on target value for a specific CloudWatch metric.
- **Step Scaling**: scale based on a CloudWatch alarm.
- **Scheduled Scaling**: scale based on a specified date/time.

## EC2 Launch Type - Auto Scaling EC2 Instance

Well explained [here](https://www.youtube.com/watch?v=0j8D-be2J1k)
- **Auto Scaling Group Scaling**
  - Scale your ASG based on CPU utilization.
  - Add EC2 instance over time.
- **EC2 Cluster Capacity Provider** (newer, better)
  - Used to automatically provision and scale the infraestructure for your ECS tasks.
  - Paired with an ASG.
  - Add EC2 Instances when you're missing capacity (CPU, RAM).
  **You can think of it as an "extension" to the ASG, it provides custom metrics to it.**
  *Fun fact, i think this is mentioned [here](https://youtu.be/i_fq7siKslo?t=360)*

## ECR (Elastic Container Registry)

- Store and manage Docker Images on AWS. 
- Private and Public (ECR Public Gallery) repository.
- Fully integrated with ECS and EKS, backed by [[S3]].
- Access controlled through IAM.
- Supports image vulnerability scanning, lifecycle, etc.


