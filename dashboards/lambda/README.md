# AWS Lambda automated dashboard

[AWS Lambda](https://aws.amazon.com/lambda/) is a serverless compute service that lets you run code without provisioning or managing servers.
Lambda automatically scales your applications and only charges for the compute time you consume.

The following graphs are displayed in this automated dashboard:

## Invocation Metrics

- [Invocations](#invocations)
- [Errors](#errors)
- [Throttles](#throttles)
- [Recursive Invocations Dropped](#recursive-invocations-dropped)

## Performance Metrics

- [Duration](#duration)
- [Post Runtime Extensions Duration](#post-runtime-extensions-duration)

## Concurrency Metrics

- [Concurrent Executions](#concurrent-executions)
- [Unreserved Concurrent Executions](#unreserved-concurrent-executions)
- [Claimed Account Concurrency](#claimed-account-concurrency)

## Provisioned Concurrency Metrics

- [Provisioned Concurrency Invocations](#provisioned-concurrency-invocations)
- [Provisioned Concurrency Spillover Invocations](#provisioned-concurrency-spillover-invocations)
- [Provisioned Concurrent Executions](#provisioned-concurrent-executions)
- [Provisioned Concurrency Utilization](#provisioned-concurrency-utilization)

## Asynchronous Invocation Metrics

- [Async Events Received](#async-events-received)
- [Async Event Age](#async-event-age)
- [Async Events Dropped](#async-events-dropped)
- [Dead Letter Errors](#dead-letter-errors)
- [Destination Delivery Failures](#destination-delivery-failures)

## Event Source Metrics

- [Iterator Age](#iterator-age)
- [Offset Lag](#offset-lag)
- [Oversized Record Count](#oversized-record-count)

## Deployment Metrics

- [Signature Validation Errors](#signature-validation-errors)

---

## Invocation Metrics

### Invocations

The "Invocations" graph shows the number of times your function code is invoked, including successful invocations and those that result in function errors.

This graph displays values from the `lambda_invocations` metric.
This metric equals the number of requests billed for the function.

### Errors

The "Errors" graph shows the number of invocations that result in a function error.

This graph displays values from the `lambda_errors` metric.
Function errors include exceptions thrown by your code and exceptions thrown by the Lambda runtime.
The runtime returns an error for issues such as timeouts and configuration errors.

To calculate the error rate, divide the value of Errors by the value of Invocations.

### Throttles

The "Throttles" graph shows the number of invocation requests that are throttled.

This graph displays values from the `lambda_throttles` metric.
When all function instances are processing requests and no concurrency is available to scale up, Lambda rejects additional requests with a throttling error (429 status code).

Throttled requests may indicate that you need to:
- Request a concurrency limit increase for your account
- Configure reserved concurrency for the function
- Implement retry logic in your application

### Recursive Invocations Dropped

The "Recursive Invocations Dropped" graph shows the number of times Lambda has stopped invocation of your function because it detected that the function is part of an infinite recursive loop.

This graph displays values from the `lambda_recursive_invocations_dropped` metric.
Lambda drops the next invocation by default after approximately 16 times in a chain of requests.

This metric helps protect your account from runaway costs due to infinite loops.
If you see this metric, review your function code for unintended recursive patterns.

---

## Performance Metrics

### Duration

The "Duration" graph shows the amount of time that your function code spends processing an event.

This graph displays values from the `lambda_duration` metric.
The billed duration for an invocation is the value of Duration rounded up to the nearest millisecond.

Duration supports percentile (p) statistics:
- p50 (median): The duration value that 50% of invocations fall below
- p95: The maximum duration of 95% of invocations, excluding the slowest 5%
- p99: The maximum duration of 99% of invocations, excluding the slowest 1%

High duration values may indicate:
- Inefficient code that needs optimization
- Cold start latency for new function instances
- Resource constraints (CPU or memory)

### Post Runtime Extensions Duration

The "Post Runtime Extensions Duration" graph shows the cumulative amount of time that the runtime spends running code in extensions after the function code has completed.

This graph displays values from the `lambda_post_runtime_extensions_duration` metric.

Extensions are external processes that augment your Lambda function.
Examples include monitoring tools, security agents, and configuration managers.
High values may indicate that extensions are adding significant overhead to your function execution.

---

## Concurrency Metrics

### Concurrent Executions

The "Concurrent Executions" graph shows the number of function instances that are processing events.

This graph displays values from the `lambda_concurrent_executions` metric.
If this number reaches your concurrent executions quota for the Region, or the reserved concurrency limit on the function, Lambda throttles additional invocation requests.

Monitor this metric to:
- Understand your function's scaling behavior
- Identify when you're approaching concurrency limits
- Plan capacity for expected load increases

### Unreserved Concurrent Executions

The "Unreserved Concurrent Executions" graph shows the number of events that are being processed by functions that don't have reserved concurrency.

This graph displays values from the `lambda_unreserved_concurrent_executions` metric.
This is an account-level metric aggregated across all functions in a Region.

This metric helps you understand how much of your account's concurrency pool is being consumed by functions without reserved concurrency.

### Claimed Account Concurrency

The "Claimed Account Concurrency" graph shows the sum of the concurrency of the functions that don't have reserved concurrency.

This graph displays values from the `lambda_claimed_account_concurrency` metric.
This represents the concurrency that is not available for functions with reserved concurrency.

---

## Provisioned Concurrency Metrics

### Provisioned Concurrency Invocations

The "Provisioned Concurrency Invocations" graph shows the number of times your function code is invoked on provisioned concurrency.

This graph displays values from the `lambda_provisioned_concurrency_invocations` metric.

Provisioned concurrency initializes a requested number of execution environments so they're ready to respond immediately to function invocations.
This eliminates cold start latency for latency-sensitive applications.

### Provisioned Concurrency Spillover Invocations

The "Provisioned Concurrency Spillover Invocations" graph shows the number of times your function code is invoked on standard concurrency when all provisioned concurrency is in use.

This graph displays values from the `lambda_provisioned_concurrency_spillover_invocations` metric.

Spillover invocations experience cold starts and higher latency.
High spillover values may indicate:
- Provisioned concurrency is set too low for the workload
- Unexpected traffic spikes
- Need to increase provisioned concurrency allocation

### Provisioned Concurrent Executions

The "Provisioned Concurrent Executions" graph shows the number of function instances that are processing events on provisioned concurrency.

This graph displays values from the `lambda_provisioned_concurrent_executions` metric.
For each invocation of an alias or version with provisioned concurrency, Lambda emits the current count.

### Provisioned Concurrency Utilization

The "Provisioned Concurrency Utilization" graph shows the percentage of allocated provisioned concurrency that is in use.

This graph displays values from the `lambda_provisioned_concurrency_utilization` metric.
For a version or alias with provisioned concurrency, the value is ProvisionedConcurrentExecutions divided by the total amount of provisioned concurrency allocated.

For example, 0.5 (50%) indicates that half of allocated provisioned concurrency is in use.

Use this metric to:
- Optimize provisioned concurrency allocation
- Identify over-provisioning that increases costs
- Detect under-provisioning that causes spillover

---

## Asynchronous Invocation Metrics

### Async Events Received

The "Async Events Received" graph shows the number of events that Lambda successfully queues for processing.

This graph displays values from the `lambda_async_events_received` metric.
This metric provides insight into the number of events that the function receives for asynchronous invocation.

### Async Event Age

The "Async Event Age" graph shows the time between when Lambda successfully queues the event and when the function is invoked.

This graph displays values from the `lambda_async_event_age` metric.
The value of this metric increases when events are being retried due to invocation failures or throttling.

High async event age may indicate:
- Function errors causing retries
- Throttling due to concurrency limits
- Capacity issues preventing timely processing

### Async Events Dropped

The "Async Events Dropped" graph shows the number of events that are dropped without successfully running the function.

This graph displays values from the `lambda_async_events_dropped` metric.
If you configure a dead-letter queue or OnFailure destination, events are sent there before they're dropped.

Events are dropped after:
- They've been retried the maximum number of times
- They've exceeded the maximum event age

### Dead Letter Errors

The "Dead Letter Errors" graph shows the number of times Lambda attempts to send an event to a dead-letter queue but fails.

This graph displays values from the `lambda_dead_letter_errors` metric.
Dead-letter errors can occur due to:
- Permissions errors (Lambda doesn't have access to the DLQ)
- Misconfigured resources (DLQ doesn't exist or is invalid)
- Size limits (event is too large for the DLQ)

### Destination Delivery Failures

The "Destination Delivery Failures" graph shows the number of times Lambda attempts to send an event to a destination but fails.

This graph displays values from the `lambda_destination_delivery_failures` metric.
For asynchronous invocation and supported event source mappings, this tracks failures to deliver events to configured destinations.

For event source mappings, Lambda supports destinations for stream sources (DynamoDB Streams and Kinesis streams).

---

## Event Source Metrics

### Iterator Age

The "Iterator Age" graph shows the age of the last record in the event for event source mappings that read from streams.

This graph displays values from the `lambda_iterator_age` metric.
The age is the amount of time between when a stream receives the record and when the event source mapping sends the event to the function.

This metric applies to:
- DynamoDB Streams
- Kinesis streams

High iterator age indicates your function is falling behind in processing stream records, which may require:
- Increasing batch size to process more records per invocation
- Increasing function timeout or memory
- Increasing parallelization factor
- Investigating function errors or performance issues

### Offset Lag

The "Offset Lag" graph shows the difference in offset between the last record written to a topic and the last record that your function's consumer group processed.

This graph displays values from the `lambda_offset_lag` metric.

This metric applies to:
- Self-managed Apache Kafka event sources
- Amazon Managed Streaming for Apache Kafka (Amazon MSK) event sources

Similar to iterator age, high offset lag indicates your function is falling behind in processing Kafka messages.

### Oversized Record Count

The "Oversized Record Count" graph shows the number of events that couldn't be processed because they exceeded the size limit.

This graph displays values from the `lambda_oversized_record_count` metric.
This metric applies to Amazon DocumentDB event sources.

Lambda has a maximum event payload size of 6 MB for synchronous invocations.
If you see this metric, you may need to:
- Reduce the size of records in your DocumentDB collection
- Split large documents into smaller ones
- Use Amazon S3 to store large payloads and pass references

---

## Deployment Metrics

### Signature Validation Errors

The "Signature Validation Errors" graph shows the number of times Lambda fails to validate the code package signature during deployment.

This graph displays values from the `lambda_signature_validation_errors` metric.

Code signing for Lambda ensures that only trusted code runs in your functions.
Signature validation errors indicate:
- The code package signature is invalid or corrupted
- The signing profile configuration doesn't match the code
- The code package has been modified after signing
