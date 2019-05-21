# Kinesis

- Streaming data is data generated continuously by a large number of data sources, typically sending data records simultaneously and in small sizes (Kb).  
  Ex: stock prices, game data, purchases from online stores, social network data (twitter), geospatial data, iot sensor data…

## Kinesis streams

- Data producers (ec2, iot, mobile phones) streams data to Kinesis streams.
- Store data for 24 hours (default), up to 7 days
- Data is contained in shards
  - 5 transactions per second for reads, up to 2 Mb/s data
  - Up to 1 000 records per second for write, up to 1 Mb/s data
  - Data capacity of stream is a function of the number of shards. Total capacity is the sum of capacity of its shards.
- Consumers (ec2 instances) can analyze the data in shards and store it in rds, dynamodb, s3, …

## Kinesis firehose

- Data producers (ec2, iot, mobile phones) streams data to Kinesis firehose
- No persistent storage
- (optional) to have lambda functions in Firehose
- Data output to somewhere safe (s3)

## Kinesis analytics

- Works with Streams and Firehose to analyze data on the fly when it comes in
