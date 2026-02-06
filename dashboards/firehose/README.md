# AWS Firehose automated dashboard

[AWS Kinesis Data Firehose](https://aws.amazon.com/kinesis/data-firehose/) is a service for delivering real-time streaming data to destinations such as Amazon S3, Amazon Redshift, Amazon OpenSearch Service, HTTP endpoints, and third-party service providers.

The following graphs are displayed in this automated dashboard:

## Delivery Metrics

- [Delivery to S3 Records](#delivery-to-s3-records)
- [Delivery to HTTP Endpoint Data Freshness](#delivery-to-http-endpoint-data-freshness)
- [Delivery to HTTP Endpoint Bytes](#delivery-to-http-endpoint-bytes)
- [Delivery to HTTP Endpoint Records](#delivery-to-http-endpoint-records)

## Ingestion Metrics

- [Incoming Requests vs Records](#incoming-requests-vs-records)
- [Incoming Bytes](#incoming-bytes)
- [Throttled Records](#throttled-records)

## API Metrics

- [Describe Delivery Stream Requests](#describe-delivery-stream-requests)
- [List Delivery Streams Latency](#list-delivery-streams-latency)
- [List Delivery Streams Requests](#list-delivery-streams-requests)

## Error & Security Metrics

- [Failed Validation Records](#failed-validation-records)
- [KMS Key Issues](#kms-key-issues)

## Performance & Limits

- [PutRecordBatch Operations](#putrecordbatch-operations)
- [Bytes Per Second Limit](#bytes-per-second-limit)
- [Records Per Second Limit](#records-per-second-limit)

---

## Delivery Metrics

### Delivery to S3 Records

The "Delivery to S3 Records" graph shows the number of records successfully delivered to Amazon S3 over the specified time period.

This graph displays values from the `firehose_delivery_to_s3_records` metric. Amazon Data Firehose emits this metric only when you enable backup for all documents.

This graph will show a line for the S3 delivery record count, allowing you to monitor successful data delivery to your S3 backup destination.

### Delivery to HTTP Endpoint Data Freshness

The "Delivery to HTTP Endpoint Data Freshness" graph shows the age (from getting into Amazon Data Firehose to now) of the oldest record in Amazon Data Firehose. Any record older than this age has been delivered to OpenSearch Service.

This graph displays values from the `firehose_delivery_to_http_endpoint_data_freshness` metric, which helps you understand data latency in your delivery pipeline.

Lower values indicate fresher data and better pipeline performance, while higher values may indicate delivery delays or backlogs.

### Delivery to HTTP Endpoint Bytes

The "Delivery to HTTP Endpoint Bytes vs Processed Bytes" graph compares the number of bytes delivered successfully to the HTTP endpoint versus the number of attempted processed bytes, including retries.

This graph displays values from the following metrics:
- `firehose_delivery_to_http_endpoint_bytes` - Successfully delivered bytes
- `firehose_delivery_to_http_endpoint_processed_bytes` - Total attempted bytes including retries

This comparison helps you understand delivery efficiency and retry patterns. A large gap between processed and delivered bytes may indicate delivery issues or high retry rates.

### Delivery to HTTP Endpoint Records

The "Delivery to HTTP Endpoint Records vs Processed Records" graph compares the number of records delivered successfully to the HTTP endpoint versus the number of attempted records including retries.

This graph displays values from the following metrics:
- `firehose_delivery_to_http_endpoint_records` - Successfully delivered records
- `firehose_delivery_to_http_endpoint_processed_records` - Total attempted records including retries

This graph will show lines for both delivered and processed record counts, allowing you to monitor delivery success rates and identify potential delivery issues.

---

## Ingestion Metrics

### Incoming Requests vs Records

The "Incoming Requests vs Records" graph compares the number of successful PutRecord and PutRecordBatch requests versus the number of records ingested successfully into the Firehose stream over the specified time period.

This graph displays values from the following metrics:
- `firehose_incoming_put_requests` - Number of API requests
- `firehose_incoming_records` - Number of records ingested

This comparison helps you understand batch efficiency - a high records-to-requests ratio indicates effective batching, while a low ratio may suggest many single-record operations.

### Incoming Bytes

The "Incoming Bytes" graph shows the number of bytes ingested successfully into the Firehose stream over the specified time period.

This graph displays values from the `firehose_incoming_bytes` metric, which helps you monitor data volume and throughput patterns.

This graph will show a line for the incoming byte count, allowing you to track data ingestion volume and identify usage patterns or potential capacity issues.

### Throttled Records

The "Throttled Records" graph shows the number of records that were throttled because data ingestion exceeded one of the Firehose stream limits.

This graph displays values from the `firehose_throttled_records` metric, which is critical for identifying when your Firehose stream is hitting capacity limits.

An increase in throttled records indicates you may need to:
- Increase your Firehose stream capacity
- Optimize your data ingestion patterns
- Consider using multiple Firehose streams

---

## API Metrics

### Describe Delivery Stream Requests

The "Describe Delivery Stream Requests" graph shows the total number of DescribeDeliveryStream requests made to your Firehose streams.

This graph displays values from the `firehose_describe_delivery_stream_requests` metric, which helps you monitor API usage patterns.

High request volumes may indicate:
- Frequent monitoring or management operations
- Application patterns that could be optimized
- Potential need for caching strategies

### List Delivery Streams Latency

The "List Delivery Streams Latency" graph shows the time taken per ListDeliveryStream operation, measured over the specified time period.

This graph displays values from the `firehose_list_delivery_streams_latency` metric, which helps you monitor API performance.

This graph will show a line for API latency, allowing you to identify performance issues or changes in AWS service response times.

### List Delivery Streams Requests

The "List Delivery Streams Requests" graph shows the total number of ListFirehose requests made to enumerate your Firehose streams.

This graph displays values from the `firehose_list_delivery_streams_requests` metric, which helps you monitor enumeration API usage.

This graph will show a line for the request count, allowing you to track how often your applications or monitoring tools enumerate Firehose streams.

---

## Error & Security Metrics

### Failed Validation Records

The "Failed Validation Records" graph shows the number of records that failed record validation.

This graph displays values from the `firehose_failed_validation_records` metric, which is critical for data quality monitoring.

An increase in failed validation records may indicate:
- Data format changes in your source systems
- Schema mismatches between source and destination
- Configuration issues in your Firehose stream

### KMS Key Issues

The "KMS Key Issues" graph shows the number of times the service encounters various KMS-related exceptions for the Firehose stream.

This graph displays values from the following metrics:
- `firehose_kms_key_access_denied` - KMSAccessDeniedException occurrences
- `firehose_kms_key_disabled` - KMSDisabledException occurrences
- `firehose_kms_key_invalid_state` - KMSInvalidStateException occurrences
- `firehose_kms_key_not_found` - KMSNotFoundException occurrences

This graph will show lines for each KMS error type, allowing you to quickly identify encryption and key management issues that may prevent data delivery.

---

## Performance & Limits

### PutRecordBatch Operations

The "PutRecordBatch Operations" graph shows the number of successful and failed PutRecordBatch operations, indicating batch processing performance and error rates.

This graph displays values from the following metrics:
- `firehose_put_record_batch_success` - Successful batch operations
- `firehose_put_record_batch_failure` - Failed batch operations

This comparison helps you understand batch operation reliability and identify patterns in batch processing failures.

### Bytes Per Second Limit

The "Bytes Per Second Limit" graph shows the current maximum number of bytes per second that a Firehose stream can ingest before throttling.

This graph displays values from the `firehose_bytes_per_second_limit` metric, which helps you understand your current throughput capacity.

This graph will show a line for the current limit, allowing you to track capacity changes and plan for scaling needs.

### Records Per Second Limit

The "Records Per Second Limit" graph shows the current maximum number of records per second that a Firehose stream can ingest before throttling.

This graph displays values from the `firehose_records_per_second_limit` metric, which helps you understand your current record rate capacity.

This graph will show a line for the current record rate limit, allowing you to monitor capacity constraints and plan for scaling requirements.
