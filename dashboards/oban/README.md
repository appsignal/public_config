# Oban automated dashboard

[Oban](https://oban.pro/) is a background job system for Elixir.

When using [the Oban integration in the AppSignal for Elixir gem](https://docs.appsignal.com/elixir/integrations/oban.html), the Oban automated dashboard will appear. This README uses the existing Oban documentation as reference.

> ⚠️ Oban version 2.0 or higher is required.

The following graphs are displayed in this automated dashboard:

- [Job duration](#job-duration)
- [Job queue time](#job-queue-time)
- [Jobs completed](#jobs-completed)
- [Job exceptions](#job-exceptions)

## Job duration

The "Job duration" graph shows the average time it took an Oban worker to complete each job it processed.

This graph displays values from the `oban_job_duration` metric. This graph will show a line for each combination of values of the following metric tags:

- The **worker** that executed each job.

## Job queue time

The "Job queue time" graph shows the 95th percentile of the time that each Oban job spent on the queue, before an Oban worker began executing it.

This graph displays values from the `oban_job_queue_time` metric. This graph will show a line for each combination of values of the following metric tags:

- The **queue** in which each job waited to be executed.

## Jobs completed

The "Jobs completed" graph shows the amount of Oban jobs that were completed successfully.

This graph displays values from the `oban_job_count` metric. This graph will show a line for each combination of values of the following metric tags:

- The **worker** that executed each job.
- The **queue** in which each job was inserted.

## Job exceptions

The "Job exceptions" graph shows the amount of Oban jobs that raised an exception or returned an error during execution.

This graph displays values from the `oban_job_count` metric. This graph will show a line for each combination of values of the following metric tags:

- The **worker** that executed each job.
