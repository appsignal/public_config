# Render automated dashboards

[Render](https://render.com/) is a cloud platform-as-a-service for running web services, background workers, persistent disks, Postgres databases and Key Value (Valkey/Redis) instances.

These dashboards display data emitted by Render's [OpenTelemetry metrics stream](https://render.com/docs/metrics-streams), forwarded to AppSignal through the AppSignal collector. The collector's Render router converts CPU, memory, disk usage, disk I/O and network I/O metrics into host metrics; the remaining `render.*` metrics are exposed as custom metrics and power these dashboards.

The following automated dashboards may appear:

- [HTTP automated dashboard](#http-automated-dashboard)
- [Postgres automated dashboard](#postgres-automated-dashboard)
- [Key Value automated dashboard](#key-value-automated-dashboard)

All three dashboards are currently marked Beta.

## HTTP automated dashboard

The "Render/HTTP" dashboard shows request volume and latency for Render web services. Render aggregates these metrics across all instances of a service, so each line corresponds to a host/status_code combination across the whole service rather than to a specific replica.

The following graphs are displayed in this automated dashboard:

- HTTP requests (broken down by status code and host)
- HTTP latency (p50/p95/p99 broken down by host and status code)

These graphs display values from the `render.service.http.requests.total` and `render.service.http.requests.latency` metrics.

## Postgres automated dashboard

The "Render/Postgres" dashboard shows information about Render Postgres instances.

The following graphs are displayed in this automated dashboard:

- Connections (active connections per database, compared against the connection limit)
- Storage size (database size and indexes size per database)
- Transaction volume
- Sequential table scans (per database)
- Transaction exhaustion (per database)
- Slow locks
- Slow lock wait time
- Replication lag (per replica host)

These graphs display values from the `render.postgres.*` metrics.

## Key Value automated dashboard

The "Render/Key Value" dashboard shows connection metrics for Render Key Value (Valkey/Redis) services. CPU, memory, disk and network usage for Key Value services are reported as host metrics and appear on the host metrics dashboard instead.

The following graphs are displayed in this automated dashboard:

- Connections (active connections compared against the connection limit)

This graph displays values from the `render.keyvalue.connections` and `render.keyvalue.connection.limit` metrics.
