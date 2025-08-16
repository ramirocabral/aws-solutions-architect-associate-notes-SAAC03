![[Pasted image 20221101205129.png]]

## Overview

- Schedule Cron jobs.
- Event Pattern: react to a service doing something.
- Triger Lambdas, send messages to SQS, SNS, etc.

## EventBridge Rules

![[eventbridge_rules.png]]

## Event Bus

- **Default Event Bus**: receives events from AWS services.
- **Partner Event Bus**: receives events from AWS SaaS Partners.
- **Custom Event Bus**: own apps can send events to this bus.
- Event Buses can be accesed by other account using Resource-Based Policies.
- Can **archive events** sent to a bus (indefinitely or set period). Ability to **replay archived events**.

## Schema Registry

- EventBridge can analyze events in a bus and infer the **schema**.
- The **Schema Registry** can generate code for an application, that will know in advance how data is structured in the bus. (like a json response from an API, you know the fileds and possible values)
- Schemas can be versioned.

## Resource-based Policy

- Permissions from a specific Event Bus.
- Use case: aggreagate all event from an Organization in a single account or region.
