# On Premise options

- Download Amazon Linux 2 AMI as VM.

## VM Import/Export

- Migrate existing applications into [[EC2]].
- Create a DR repository stragegy for your on premise VMs.
- Can export back from EC2 to on premise.

## AWS Application Discovery Service

- Plan migration projects by gathering information about on-premises data centers.
- Server utilzation and dependecy mappings.
- **Agentless Discovery**:  (AWS Agentless Discovery Connector)
  - VM inventory, configuration, and performance history such as CPU, mem and disk.
- **Agent-based Discovery**:  (AWS Application Discovery Agent)
  - System config, system performance, processes and details of network connections.
- Resulting data can be viewed within AWS Migration Hub.

## AWS Application Migration Service (MGN)

- Lift-and-shift (rehost) solution, simplified **migrating** apps to AWS.
- Converts physical, virtual and (other) cloud-based servers to run on AWS.
- Continuous replication.
- Minimal downtime, reduced costs.

## AWS SMS (Server migration service)

- Incremental replication of on premise live servers to AWS.

## Outposts

- **Server Racks** that offer the AWS APIs and tools to build your apps on-premise just as in the cloud.
- AWS will setup and manage **Outposts Racks** within your on-premise infra.
