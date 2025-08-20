# Disaster Recovery

- **RPO**: Recovery Point Objective.
  - The maximum acceptable amount of data loss measured in time.
- **RTO**: Recovery Time Objective.
  - The maximum acceptable amount of time to restore the system after a disaster. (downtime)

## DR Strategies

- Backup and Restore.
- Pilot Light.
- Warm Standby.
- Hot Site / Multi Site approach.

## Backup and Restore

- **High RPO and RTO**.
- Cheap.

![[backup_and_restore.png]]

## Pilot Light

- A small version of the app is always running in the cloud.
- useful for the critical core.
- Faster than Backup and Restore, critical systems are already up.

![[pilot_light.png]]

## Warm Standby

- Full system is up and running, but at a minimum size.
- Upon disaster, we can scale it.

![[warm_standby.png]]

## Hot Site / Multi Site

- Very low RTO.
- Very expensive.
- Full Prod Scale running in AWS and on-premise.
- Active-active.

![[multi_site.png]]
