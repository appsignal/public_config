# Heroku automated dashboards

[Heroku](https://www.heroku.com/) is a cloud platform-as-a-service that allows you to easily deploy your applications and their dependencies.

This README uses the existing [Heroku dashboards documentation](https://docs.appsignal.com/heroku/dashboards.html) as reference.

When using [the AppSignal Heroku log drain](https://docs.appsignal.com/heroku/setup-logdrain.html) to send data about your Heroku application to AppSignal, the following automated dashboards may appear:

- [Status automated dashboard](#status-automated-dashboard)
- [Redis automated dashboard](#redis-automated-dashboard)
- [PostgreSQL automated dashboard](#postgresql-automated-dashboard)

## Status automated dashboard

The "Heroku Status" dashboard will show information about the response status codes emitted by your Heroku application.

The following graphs are displayed in this automated dashboard:

- [Status codes](#status-codes)

### Status codes

The "Heroku status codes" graphs show the status codes that Heroku replied to in response to incoming HTTP requests. The first graph shows the total amount of responses for a given status code, while the second one shows the relative percentage of responses with a given status code. The status codes are grouped by their range (2xx, 3xx, ...)

These graphs display values from the `heroku_status` metric. These graphs will show a line for each combination of values of the following metric tags:

- The status **code** that was sent as a response.

## Redis automated dashboard

The "Heroku Redis" dashboard will show information about the premium Redis instances deployed in Heroku for your application.

> ⚠️ This dashboard will only appear for applications that have a premium Redis instance deployed with Heroku.

The following graphs are displayed in this automated dashboard:

- [Active connections](#active-connections)
- [Hit rate](#hit-rate)
- [Evicted keys](#evicted-keys)
- [Memory](#memory)
- [Server load average](#server-load-average)
- [Server I/O](#server-io)
- [Server memory](#server-memory)

### Active connections

The "Active connections" graph shows the number of connections currently established on the Redis instance.

This graph displays values from the `redis_active_connections` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Hit rate

The "Hit rate" graph shows the ratio of successful reads out of all read operations. When using Redis as an intermediate cache, this shows the amount of operations for which the requested value was successfully cached by Redis.

This graph displays values from the `redis_hit_rate` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Evicted keys

The "Evicted keys" graph shows the number of keys that were automatically removed from your Redis instance, due to it reaching its configured memory limit.

This graph displays values from the `redis_evicted_keys` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Memory

The "Memory" graph shows the approximate amount of memory that was used by your Redis processes, including the shared buffer cache and the memory required for each active connection.

This graph displays values from the `memory` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Server load average

The "Server load average" graph shows the average CPU load on the Redis server.

This graph displays values from the `load_avg` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Server I/O

The "Server I/O" graph shows the amount of read and write I/O operations (in 16kB blocks) performed by your Redis server.

This graph displays values from the `read_iops` and `write_iops` metrics. This graph will show a line for each metric's combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Server memory

The "Server memory" graph shows the memory status on your Redis server. It shows the memory currently in use, the free memory, and the memory in use by the operating system for page caches.

This graph displays values from the `memory` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.
- The **state**, which is either:
  - "total", the memory currently in use
  - "free"
  - "cached"

## PostgreSQL automated dashboard

The "Heroku Postgres" dashboard will show information about the PostgreSQL instances deployed in Heroku for your application.

> ⚠️ This dashboard will only appear for applications that have a PostgreSQL instance deployed with Heroku.

The following graphs are displayed in this automated dashboard:

- [Database size](#database-size)
- [Tables](#tables)
- [Index cache hit rate](#index-cache-hit-rate)
- [Table cache hit rate](#table-cache-hit-rate)
- [Active connections](#active-connections)
- [Waiting connections](#waiting-connections)
- [Memory](#memory)
- [Server load average](#server-load-average)
- [Server I/O](#server-io)
- [Server memory](#server-memory)

### Database size

The "Database Size" graph represents the number of bytes of data corresponding to your database on disk, including all indexes and table contents.

This graph displays values from the `db_size` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Tables

The "Tables" graph represents the number of tables in the database.

This graph displays values from the `tables` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Index cache hit rate

The "Index Cache Hit Rate" graph represents the ratio of index lookups that are successfully resolved by consulting the shared buffer cache.

This graph displays values from the `index_cache_hit_rate` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Table cache hit rate

The "Table Cache Hit Rate" graph represents the ratio of index lookups that are successfully resolved by consulting the shared buffer cache.

This graph displays values from the `table_cache_hit_rate` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Active connections

The "Active Connections" graph represents the number of active connections established on the database.

This graph displays values from the `active_connections` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Waiting connections

The "Waiting Connections" graph represents the number of connections waiting to be established on the database. If many connections are waiting to be established, this might indicate a problem with your database's concurrency configuration.

This graph displays values from the `waiting_connections` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the Redis instance from which this metric is sourced.

### Memory

The "Memory" graph shows the approximate amount of memory that was used by your PostgreSQL processes, including the shared buffer cache and the memory required for each active connection.

This graph displays values from the `memory` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the PostgreSQL instance from which this metric is sourced.

### Server load average

The "Server load average" graph shows the average CPU load on the PostgreSQL server.

This graph displays values from the `load_avg` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the PostgreSQL instance from which this metric is sourced.

### Server I/O

The "Server I/O" graph shows the amount of read and write I/O operations (in 16kB blocks) performed by your PostgreSQL server.

This graph displays values from the `read_iops` and `write_iops` metrics. This graph will show a line for each metric's combination of values of the following metric tags:

- The **source**, the PostgreSQL instance from which this metric is sourced.

### Server memory

The "Server memory" graph shows the memory status on your PostgreSQL server. It shows the memory currently in use, the free memory, and the memory in use by the operating system for page caches.

This graph displays values from the `memory` metric. This graph will show a line for each combination of values of the following metric tags:

- The **source**, the PostgreSQL instance from which this metric is sourced.
- The **state**, which is either:
  - "total", the memory currently in use
  - "free"
  - "cached"
