# Ecto automated dashboard

[Ecto](https://hexdocs.pm/ecto/Ecto.html) is the database wrapper and query generator for Elixir.

When using [the Ecto integration in the AppSignal for Elixir package](https://docs.appsignal.com/elixir/integrations/ecto.html), the Ecto automated dashboard will appear.

The following graphs are displayed in this automated dashboard:

- [Query time](#query-time)
- [Throughput](#throughput)
- [Total time](#total-time)
- [Decode time](#decode-time)
- [Queue time](#queue-time)
- [Idle time](#idle-time)
- [Total time per host](#total-time-per-host)

## Query time

The "Query time" graph shows the 95th percentile of the time the database spent executing each query, per table.

This graph displays values from the `ecto_query_time` metric. This graph will show a line for each combination of values of the following metric tags:

- The **repo** that issued each query.
- The **source** (table name) each query touched.

## Throughput

The "Throughput" graph shows how many queries were issued per table.

This graph displays the count field of the `ecto_query_time` metric. This graph will show a line for each combination of values of the following metric tags:

- The **repo** that issued each query.
- The **source** (table name) each query touched.

## Total time

The "Total time" graph shows the 95th percentile of total Ecto time per table. Total time is the sum of queue, query and decode time.

This graph displays values from the `ecto_total_time` metric. This graph will show a line for each combination of values of the following metric tags:

- The **repo** that issued each query.
- The **source** (table name) each query touched.

## Decode time

The "Decode time" graph shows the mean time spent decoding query results into Elixir terms, per table. Tables with wide rows or large binary fields will typically have higher decode times.

This graph displays values from the `ecto_decode_time` metric. This graph will show a line for each combination of values of the following metric tags:

- The **repo** that issued each query.
- The **source** (table name) each query touched.

## Queue time

The "Queue time" graph shows the 95th percentile of time each query spent waiting for a database connection from the pool, per host. High values usually indicate pool saturation on that node.

This graph displays values from the `ecto_queue_time` metric. This graph will show a line for each combination of values of the following metric tags:

- The **repo** that issued each query.
- The **hostname** that issued each query.

## Idle time

The "Idle time" graph shows the mean time connections sat idle in the pool before being checked out, per host. Consistently low values indicate the pool is heavily used; consistently high values suggest the pool is over-sized for the traffic on that node.

This graph displays values from the `ecto_idle_time` metric. This graph will show a line for each combination of values of the following metric tags:

- The **repo** that issued each query.
- The **hostname** that issued each query.

## Total time per host

The "Total time per host" graph shows the mean total Ecto time per host. Useful for spotting nodes whose database performance has degraded relative to peers.

This graph displays values from the `ecto_total_time` metric. This graph will show a line for each combination of values of the following metric tags:

- The **repo** that issued each query.
- The **hostname** that issued each query.
