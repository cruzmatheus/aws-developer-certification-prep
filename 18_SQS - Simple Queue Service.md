# SQS - Simple Queue Service

## Standard Queue
- Oldest offering (over 1- years old)
- Fully managed
- Scales from 1 to 10.000 messages per second
- Default retention: 4 days, maximum of 14 days
- No limit to how many messages can be in the queue
- Low latency (< 10ms on publish and receive)
- Horizontal consumer scaling
- Can have duplicates (at least once, occasionally)
- Can have out of order messages (best effort ordering)
- Limitation of 256KB per message sent

## Delay Queue
- Delay a message up to 15 minutes (consumer don't see it immediately)
- Default delay is 0 seconds (message is available right away)
- Can set a default at queue level
- Can override the default using the <u>DelaySeconds</u> parameter

## Producing Messages
A message has:
- Body
- Attributes (metadata - optional)
- Delay delivery (optional)

The result of message producing are:
- Message identifier
- MD5 hash of the body

## Consuming messages
- Poll SQS for messages
- Can receive up to 10 messages at a time
- Process the mressage within the visibility timeout
- After read, the consumer deletes the message using the message ID and receipt handle

## Visibility timeout
It's locking mechanism to avoid more than one consumer reading the same message

- Default value is 30 seconds
- Can be between 0 seconds and 12 hours
- In case of processing error, the consumer will wait until the end of the visibility timeout to be able to read the message again
- If the message could not be fully processed during this time windows another consumer can read the same message (more than once)
- <b>ChangeMessageVisibility</b> change visibility time via API
- <b>DeleteMessage</b> API is used to delete the message after processing

## Dead Letter Queue - DLQ

Contains all the messages that entered in a failure loop during the normal processing.

- Redrive policy: Threshold of how many times a message can fail during processing, before go to the DLQ
- Should be created before the it's utilization
- Max retention period is 14 days

## Long polling

- If the queue is empty, the consumer will wait for a defined period until a message arrives
- It decreases the number of API calls made to SQS while increasing the efficiency and latency of the application
- The wait time can be between 1 seconds to 20 seconds
- Long polling is prefirable to Short polling
- Can be enabled at queue level or at the API level using <b>WaitTimeSeconds</b>

## FIFO Queue
First in - First out

- Not available in all regions
- Queue name must end in .fifo
- Lower throughput (up to 3000 per second with batching, 300/s without)
- Messages are processed in order by the consumer
- Messages are sent exactly once
- No per message delay (only per queue)

### Deduplication
Not sending the same message twice

- Provide a <b>MessageDeduplicationId</b> with the message
- De-duplication interval is 5 minutes
- <b>Content Based Duplication</b>: the MessageDeduplicationId is generated as the SHA-256 of the message body (configured at queue level)


### Sequencing
To ensure strict ordering between messages

- A <b>MessageGroupId</b> must be specified
- Messages with different group id may be received out of order
- Messages with the same group id are delivered to one consumer at a time

## SQS Extended Client
Used to send messages larger than 256KB

- Java library
- Message is sent to S3 than a small message with metadata is sent to SQS
- The consumer consumes the metadata message and retrieve the message in S3 bucket

## Security

- Encryption in flight using HTTPS
- Can enable Server Side Encryption (SSE) using KMS
- IAM policy must allow usage of SQS
- SQS queue access policy