# Elastic Map Reduce

## Overview

- Run big data frameworks
- Hadoop clusters (big data).
- Cluster can be made of **hundreds of [[EC2]] instances**.
- Comes with Apache Spark, HBase, Presto, Flink.
- Takes care of provisioning and configuration.
- Auyto-saling and integrated with Spot Instances.

- **Use case: data processing, machine learning, web indexing, big data..**

## Nodes

- **Master Node**: manages the cluster and health - long running.
- **Core Node**: Run tasks and store data - long running.
- **Task Node**: just runs tasks (spot instances).
- Can have long-running cluster, or transient cluster.

## Purchasing options

- On demand: reliable, predictable, won't be terminated.
- Reserved (min 1 year): cost savings. Useful for master and core nodes.
