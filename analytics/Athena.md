![[athena.webp]]

## Overview

- Serverless.
- Uses SQL.
- Interactive query serve to analyze data in S3.
- Pay only per queries run.
- Process logs.
- Store results back to [[S3]].

## Supported Data types

- CSV.
- JSON.
- ORC.
- Avro.
- Parquet (faster than csv).

## Pricing

- 5 Dollar per TB scanned

## Performance Improvement

- Use **columnar data** for cost-savings (less scan).
  - Parquet or ORC is recommended.
  - Huge performance improvement.
  - Use Glue to convert data to Parquet or ORC.
- **Compress data** for smaller retrievals.
- Partition datasets in S# for easy querying on virtual columns.
  - Example: s3://athena-examples/flight/parquet/year=1991/month=1/day=1/
- Use **larger files** for better performance.


## Federated query

- Query data from outside from [[S3]].
- Uses Data Source Connectors ([[Lambda]] functions that connects to another service).
