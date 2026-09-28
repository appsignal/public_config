# Redis automated dashboard

[Redis](https://redis.io/) is an in-memory data store, used by most application stacks as a cache, a session store, and the backing store for job queues such as Sidekiq, Oban and BullMQ.

This dashboard displays data collected by the [OpenTelemetry Collector's Redis receiver](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/receiver/redisreceiver), forwarded to AppSignal through the AppSignal collector. The receiver reads Redis' own `INFO` output and emits it as OpenTelemetry metrics, so no Redis configuration is required beyond granting the collector read access.

This dashboard covers self-hosted and self-managed Redis. Managed Redis on Heroku and AWS is already covered by the [Heroku Redis](../heroku/) and [AWS ElastiCache Redis](../aws/) dashboards, which read from those providers' own metric streams.

The dashboard is created when AppSignal receives the `redis.commands.processed` metric.

## Redis automated dashboard

The "Redis" dashboard is ordered by urgency of signal: the failure and saturation indicators come first, then memory and throughput, then operational context.

The following graphs are displayed in this automated dashboard:

- Rejected connections
- Evicted keys
- Blocked clients
- Keyspace hits vs misses
- Expired keys
- Memory used (used, RSS and peak)
- Memory fragmentation ratio
- Commands processed
- Network throughput (in and out)
- Connected clients
- Connections received
- Keyspace size per database (keys and keys with an expiration)
- Connected replicas
- Changes since last save

These graphs display values from the `redis.*` metrics.

### Monitoring more than one instance

AppSignal builds metric tags from OpenTelemetry data point attributes. The Redis receiver reports the instance it scraped as *resource* attributes (`redis.version`, and optionally `server.address` and `server.port`), and the collector lifts resource attributes onto data points only for Render and Heroku. Metrics from several Redis instances therefore merge into a single line per chart.

Do not work around this by copying resource attributes onto data points with a `transform` processor. This dashboard matches each metric on its exact tag set, so adding a tag stops the charts matching anything at all. To separate instances today, send each one to its own AppSignal app.

This dashboard is currently marked Beta.
