# Timestream
- Time series database.
- Fully managed.
- Scalable.
- Store and analyze trillions of events per day.
- Full SQL compatibilty.
- Recent and historical data diffrent storage tiers.
- support encrypt in transit and at rest.

## Use cases 

- IOT
- operational apps
- real time analytics

## Architecture

### Sources
- Lambda
- AWS Iot
- Kinesis data analytics for apache flink
- prometheus (3rd party) (monitoring metrics)
- telegraph (3rd party) (metrics)

### Targets
- quicksight
- sage maker
- grafana (Monitoring Dashboard)
- any jdbc connection
