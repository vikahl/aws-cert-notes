# Kinesis

Definitions

- Streaming data is data generated continuously by a large number of data sources, typically sending data records simultaneously and in small sizes (KB).  
  Ex: stock prices, game data, purchases from online stores, social network data (twitter), geospatial data, iot sensor data…

## Kinesis streams

- Data producers (EC2, iot, mobile phones) streams data to Kinesis streams.
- Data is stored for 24 hours by default, can be stored up to 7 days
- Data is contained in shards
  - Data capacity of stream is a function of the number of shards.
  - Total capacity is the sum of capacity of its shards.
- Consumers (EC2 instances) can analyse the data in shards and store it in RDS, DynamoDB, S3, …
- Limits:
  - Read: 5 transactions per second, up to 2 MB/s data
  - Write: Up to 1 000 records per second, up to 1 MB/s data

## Kinesis Firehose

- Data producers (EC2, iot, mobile phones) streams data to Kinesis Firehose
- Lacks persistent storage
- Possible to have Lambda functions in Firehose that processes data directly
- Data should be outputted to somewhere safe (S3)

## Kinesis analytics

- Works with Streams and Firehose to analyse data on the fly when it comes in
