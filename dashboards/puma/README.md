# Puma magic dashboard

[Puma](https://puma.io/) is a web server for Rack-based Ruby web applications.

When using [the Puma integration in the AppSignal for Ruby gem](https://docs.appsignal.com/ruby/integrations/puma.html), the Puma magic dashboard will appear. This README uses the existing Puma documentation as reference.

> ⚠️ Puma version 3.11.4 or higher is required.

The following graphs are displayed in this magic dashboard:

- [Threads](#threads)
- [Connection backlog](#connection-backlog)
- [Pool capacity](#pool-capacity)
- [Worker info](#worker-info)

## Threads

The "Threads" graph shows [information about the threads spawned by Puma to serve web requests](https://github.com/appsignal/appsignal-ruby/blob/965fe4b731c3f9a992752448e54869957215f21a/lib/puma/plugin/appsignal.rb#L109-L110), aggregated across all Puma workers. In order to serve web requests, Puma will spawn more threads when needed.

The "running" thread count refers to the threads that are currently running, either serving requests or ready to serve requests, while the "max" thread count refers to the maximum amount of threads that the Puma server is configured to spawn if needed.

This graph displays values from the `puma_threads` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric. 
- The **type**, the thread count that the line refers to:
  - `"running"`
  - `"max"`

## Connection backlog

The "Connection backlog" graph shows [the amount of incoming connections to the server](https://github.com/appsignal/appsignal-ruby/blob/965fe4b731c3f9a992752448e54869957215f21a/lib/puma/plugin/appsignal.rb#L107) that are in the server's backlog queue, waiting to be served. 

This graph displays values from the `puma_connection_backlog` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric.

## Pool capacity

The "Pool capacity" graph shows the amount of Puma threads that are available to receive requests. This includes Puma threads that have not been spawned yet.

This graph displays values from the `puma_pool_capacity` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric.

## Worker info

The "Puma worker info" graph shows the amount of Puma workers split by their current state.

The "count" shows the total number of workers running, while "booted" and "old" show, respectively, the amount of workers running the current version of your application and its configuration, and the amount of workers running a previous version of your application and its configuration.

During a deploy, the latter should be phased out by Puma as new workers are booted.

This graph displays values from the `puma_workers` metric. This graph will show a line for each combination of values of the following metric tags:

- The **hostname** of the machine that emitted the metric. 
- The **type**, the worker count that the line refers to:
  - `"count"`, the total number of workers
  - `"booted"`
  - `"old"`
