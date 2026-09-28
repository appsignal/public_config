# MySQL automated dashboard

[MySQL](https://www.mysql.com/) is a relational database, and along with [MariaDB](https://mariadb.org/) is one of the two databases most commonly paired with Rails, Phoenix and Node.js applications.

This dashboard displays data collected by the [OpenTelemetry Collector's MySQL receiver](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/receiver/mysqlreceiver), forwarded to AppSignal through the AppSignal collector. The receiver reads `SHOW GLOBAL STATUS` and the performance schema, so it works against MySQL and MariaDB alike, as well as managed instances that allow a read-only monitoring user.

The dashboard is created when AppSignal receives the `mysql.uptime` metric.

## MySQL automated dashboard

The "MySQL" dashboard is ordered by urgency of signal: lock contention and temporary tables first, because those are what turn a healthy server into a slow one, then InnoDB buffer pool health, then throughput and operational context.

The following graphs are displayed in this automated dashboard:

- Connection errors
- Row lock waits
- Row lock wait time
- Slow queries
- Table locks (immediate and waited)
- Temporary resources created (disk tables, files and tables)
- Threads (cached, connected, created and running)
- Buffer pool usage (clean and dirty pages, against the configured limit)
- Buffer pool operations
- Buffer pool pages
- Query throughput
- Commands
- Row operations (read, inserted, updated and deleted)
- Handler requests
- InnoDB I/O operations
- Log operations
- Sorts
- Opened resources
- Uptime

These graphs display values from the `mysql.*` metrics.

### Metrics you must enable on the receiver {#metrics-you-must-enable-on-the-receiver}

Five of the charts above read metrics the receiver does not emit by default. They cover query throughput, slow queries and connection errors, which MySQL monitoring guidance treats as first-order signals, so the [setup documentation](https://docs.appsignal.com/collector/infrastructure/mysql) enables them:

| Metric | Chart |
|---|---|
| `mysql.connection.errors` | Connection errors |
| `mysql.query.slow.count` | Slow queries |
| `mysql.query.count` | Query throughput |
| `mysql.query.client.count` | Query throughput |
| `mysql.commands` | Commands |

They need no grants beyond the ones the setup documentation already asks for. If you leave them disabled the rest of the dashboard still works and these charts stay empty.

### Metrics not shown on this dashboard

The receiver also emits `mysql.table.io.wait.*` and `mysql.index.io.wait.*`. These carry a tag per table, schema and index, so they produce a line per table or index and are left off the dashboard to keep it readable. They remain available for [custom dashboards](https://docs.appsignal.com/metrics/dashboards), where you can filter them to the tables you care about.

Their `*.time` variants are reported in nanoseconds rather than the milliseconds AppSignal's duration formatter expects, so chart them with the number format.

### Monitoring more than one server

AppSignal builds metric tags from OpenTelemetry data point attributes. The MySQL receiver reports the server it scraped as *resource* attributes (`mysql.instance.endpoint`, `server.address`, `server.port`), and the collector lifts resource attributes onto data points only for Render and Heroku. Metrics from several servers therefore merge into a single line per chart.

Do not work around this by copying resource attributes onto data points with a `transform` processor. This dashboard matches each metric on its exact tag set, so adding a tag stops the charts matching anything at all. To separate servers today, send each one to its own AppSignal app.

This dashboard is currently marked Beta.
