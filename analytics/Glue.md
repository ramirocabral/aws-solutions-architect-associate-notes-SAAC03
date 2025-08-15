## TLDR

Managed **extract, transform, and load (ETL)** service.

## Overview

- Prepare and transform data for analytics.
- Serverless.

### Data Catalog

The Glue Data Crawler will crawl for data stored in S3, RDS, DDB, JDBC and send the metadata to the Glue Data Catalog.

### Job Bookmarks

Prevent re-processing old data.

### DataBrew

Clean and normalize data using pre-built transformations.

### Streaming ETL

Built on Apache Spark, compatible with Kinesis Data Streaming, Kafka, and MSK.(managed Kafka)

## Example: convert data into Parquet

![[glue_parquet.png]]
