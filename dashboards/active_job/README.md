# ActiveJob automated dashboard

[ActiveJob](https://guides.rubyonrails.org/active_job_basics.html) is the background job system built for Ruby on Rails.

When using [the AppSignal for Ruby gem](https://docs.appsignal.com/ruby/integrations/mongodb.html) in an application that uses ActiveJob, the ActiveJob automated dashboard will appear.

The following graphs are displayed in this automated dashboard:

- [Job status per queue](#job-status-per-queue)
- [Job status per queue with priority](#job-status-per-queue-with-priority)
- [Throughput per job class](#throughput-per-job-class)
- [Duration per job class](#duration-per-job-class)

## Job status per queue

The "Job status per queue" graph shows the amount of jobs that were executed, grouped by their resulting status, and by the queue in which they were enqueued.

This graph displays values from the `active_job_queue_job_count` metric. This graph will show a line for each combination of values of the following metric tags:

- The **status** of the job that was executed, either:
  - "processed" (including failed)
  - "failed"
- The **queue** in which the job was enqueued. 

## Job status per queue with priority

The "Job status per queue with priority" graph shows the amount of jobs that were executed, grouped by their resulting status, by the queue in which they were enqueued, and by the priority that was given to them.

> ⚠️ The metric for this graph will only be emitted if the jobs enqueued in your ActiveJob system have a priority value assigned to them. If the jobs do not have a priority value, this graph will be empty.

This graph displays values from the `active_job_queue_priority_job_count` metric. This graph will show a line for each combination of values of the following metric tags:

- The **status** of the job that was executed, either:
  - "processed" (including failed)
  - "failed"
- The **queue** in which the job was enqueued. 
- The **priority** that was given to the job.

## Throughput per job class

The "Throughput per job class" graph shows the amount of jobs that were executed, grouped by the class that defines the job.

This graph displays values from the `transaction_duration` metric. This graph will show a line for each combination of values of the following metric tags:

- The **action** that defines the job, which includes the class in which the action is defined. 

## Duration per job class

The "Duration per job class" graph shows the amount of time that it took for jobs to execute, grouped by the class that defines the job.

This graph displays values from the `transaction_duration` metric. This graph will show a line for each combination of values of the following metric tags:

- The **action** that defines the job, which includes the class in which the action is defined. 
