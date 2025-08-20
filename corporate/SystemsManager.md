![[Pasted image 20221031093822.png]]
# AWS Systems Manager

## TLDR

Systems Manager is a collection of services and tools to help day to day ops work 

## Services

### Run Command

- Execute a command or script across multiple [[EC2]] instances.
- No need for SSH.
- Command output can be sent to [[S3]] or [[CloudWatch]] Logs.
- Send notifications to [[SNS]].
- Can be invoked with [[EventBridge]].

### Patch Manager

- Automates the process of patching managed instances.
- OS updates, apps updates and security updates.
- Patch on-demand or on a schedule using **Maintenance Windows**.
- Scan instances and get reports.

### Automation

- Simplifies common maintenanc and deployment tasks on [[EC2]] instances and other AWs resources.
- E.g restart instances, create an AMI, EBS Snapshots.
- Runbooks -> Document to define actions. (pre-defined or custom)

### OpsCenter


- Used Review and manage ops items (which are like jira tickets) these can be created by aws on auto detected failiure
- Create and maintain Runbooks to solve problems and define standard ops procedures 
