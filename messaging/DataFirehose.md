![[firehose.png]]

- **Producers**: Apps/Clients/SDKs/Data Streams/Cloudwatch.
- Fully managed. Automatic scaling, pay for what you use.
- **Near Real-Time** with buffering capability based on size/time.
- Batch writes to buffer and then S3/Redshift/OpenSearch, 3rd-party services or Custom Destinations.
- Conversions to Parquest/ORC, compressions with gzip/snappy.
- Data can be transformed with Lambdas.

## Kinesis Data Streams vs Data Firehose

- **Kinesis Data Streams**: 
  - Streaming data collection.
  - Producer-Consumer mode.
  - Real-time.
  - Provisioned/on-demand mode.
  - Data storage up to 365 days.
  - Replay Capability.
- **Data Firehose**: 
  - Load streaming data into S3/Redshift...
  - Fully managed.
  - Near real-time.
  - Automatic scaling.
  - No data storage.
  - Doesn't support replay capability.
