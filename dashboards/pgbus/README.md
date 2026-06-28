# Pgbus automated dashboard

[Pgbus](https://github.com/mhenrixon/pgbus) is a PostgreSQL-native job processing and event bus for Rails, built on [PGMQ](https://github.com/pgmq/pgmq).

When using the AppSignal integration that ships with the pgbus gem (enabled automatically when the `appsignal` gem is loaded), the Pgbus automated dashboard will appear. Pgbus reports metrics through an `ActiveSupport::Notifications` subscriber and a minutely probe. See the [pgbus AppSignal integration](https://github.com/mhenrixon/pgbus/blob/main/lib/pgbus/integrations/appsignal.rb) for the full list of metrics.

The following graphs are displayed in this automated dashboard:

- [Job status per queue](#job-status-per-queue)
- [Throughput per job class](#throughput-per-job-class)
- [Duration per job class](#duration-per-job-class)
- [Queue depth](#queue-depth)
- [Queue latency](#queue-latency)
- [Dead letter queue depth](#dead-letter-queue-depth)
- [Worker / Process count](#worker--process-count)
- [Messages sent / read](#messages-sent--read)
- [Event handler status](#event-handler-status)
- [Worker recycling](#worker-recycling)
- [Database health](#database-health)
- [Stream broadcasts](#stream-broadcasts)

## Job status per queue

The "Job status per queue" graph shows the number of jobs that were processed, failed, or dead-lettered, broken down per queue.

This graph displays values from the `pgbus_queue_job_count` metric. This graph will show a line for each combination of values of the following metric tags:

- The **queue** in which each job was enqueued.
- The **status** of the job (`processed`, `failed`, or `dead_lettered`).

## Throughput per job class

The "Throughput per job class" graph shows the number of jobs executed per job class.

This graph displays the `count` field of the `transaction_duration` metric, filtered to the `background` namespace, with a line per **action** (job class).

## Duration per job class

The "Duration per job class" graph shows the mean execution time per job class.

This graph displays the `mean` field of the `transaction_duration` metric, filtered to the `background` namespace, with a line per **action** (job class).

## Queue depth

The "Queue depth" graph shows the total number of messages waiting in each queue.

This graph displays values from the `pgbus_queue_depth` metric. This graph will show a line for each combination of values of the following metric tags:

- The **queue** being measured.
- The **hostname** of the process that reported the metric.

## Queue latency

The "Queue latency" graph shows the age of the oldest message in each queue, in milliseconds. High latency means consumers can't keep up with the rate of incoming messages.

This graph displays values from the `pgbus_queue_latency` metric. This graph will show a line for each combination of values of the following metric tags:

- The **queue** being measured.
- The **hostname** of the process that reported the metric.

## Dead letter queue depth

The "Dead letter queue depth" graph shows the number of messages that exceeded their max retries and were routed to a dead letter queue.

This graph displays values from the `pgbus_dlq_depth` metric, with a line per **hostname**.

## Worker / Process count

The "Worker / Process count" graph shows the number of active pgbus supervisor processes.

This graph displays values from the `pgbus_active_processes` metric, with a line per **hostname**.

## Messages sent / read

The "Messages sent / read" graph shows PGMQ message throughput: how many messages were enqueued (`pgbus_messages_sent`) and dequeued (`pgbus_messages_read`).

Both metrics show a line per **queue**.

## Event handler status

The "Event handler status" graph shows the number of processed and failed event-bus handler invocations.

This graph displays values from the `pgbus_event_count` metric. This graph will show a line for each combination of values of the following metric tags:

- The **handler** class that processed each event.
- The **status** of the invocation (`processed` or `failed`).

## Worker recycling

The "Worker recycling" graph shows the number of worker recycle events, broken down by reason.

This graph displays values from the `pgbus_worker_recycled` metric, with a line per **reason** (`max_jobs`, `max_memory`, or `max_lifetime`). Pgbus recycles workers on these thresholds to prevent unbounded memory growth.

## Database health

The "Database health" graph shows the number of dead tuples in queue/archive tables (`pgbus_total_dead_tuples`) and how many tables currently need a vacuum (`pgbus_tables_needing_vacuum`).

Both metrics show a line per **hostname**. These are indicators of MVCC pressure on the PGMQ queue tables.

## Stream broadcasts

The "Stream broadcasts" graph shows the number of Turbo Stream broadcasts over the last 60 minutes (`pgbus_stream_broadcasts_60m`) and the number of active SSE connections (`pgbus_stream_active_connections`).

Both metrics show a line per **hostname**.
