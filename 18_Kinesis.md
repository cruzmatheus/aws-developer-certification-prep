# Kinesis

It's a managed alternative to Apache Kafka

- Great for real-time big data
- Great for streamming frameworks
- Uses DynamoDB to store the offsets


## Types

- Kinesis Streams: low latency streaming ingest at scale
- Kinesis Analytics: perform real-time analytics on streams using SQL
- Kinesis Firehose: load streams into S3, Redshift, ElasticSearch...

### Kinesis Streams

- Are diveded in ordered Shards/Partitions
- Data retention is 1 day by default, can go up to 7 days
- Ability to reprocess data
- Multiple application can consume the same stream
- Once data is inserted into Kinesis, it can't be deleted

#### Kinesis Stream Shards

- Records are ordered PER SHARD
- One stream is made of many different shards
- 1MB/s or 1000 messages/s at write PER SHARD
- 2MB/s at read PER SHARD
- Billing is per shard provisioned

## Security

- Control access/authorization using IAM policies
- Encryption in flight using HTTPS endpoints
- Encryption at rest using KMS
- Possibility to encrypt/decrypt data client side
- VPC Endpoints available for Kinesis to access within VPC