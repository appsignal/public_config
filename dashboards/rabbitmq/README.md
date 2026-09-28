# RabbitMQ automated dashboard

[RabbitMQ](https://www.rabbitmq.com/) is a message broker, used to pass work between services and to back job queues in Elixir, Node.js and Python applications. AppSignal already instruments the client side through [amqplib](https://docs.appsignal.com/nodejs/3.x/integrations/amqplib) for Node.js and [pika](https://docs.appsignal.com/python/instrumentations/pika) for Python; this dashboard covers the broker itself.

This dashboard displays data collected by the [OpenTelemetry Collector's RabbitMQ receiver](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/receiver/rabbitmqreceiver), forwarded to AppSignal through the AppSignal collector. The receiver reads RabbitMQ's management API, so the [management plugin](https://www.rabbitmq.com/management.html) must be enabled on the broker.

The dashboard is created when AppSignal receives the `rabbitmq.message.published` metric.

## Required collector configuration

**This dashboard requires a `transform` processor in your collector config.** It is not optional, and the charts stay empty without it.

The RabbitMQ receiver reports the queue a metric belongs to as a *resource* attribute (`rabbitmq.queue.name`), and AppSignal builds metric tags from data point attributes only. Left alone, every queue on the broker reports under the same series, so their cumulative counters are deltaed against each other and the resulting numbers are meaningless rather than merely coarse.

Copy the queue name onto the data points before exporting:

```yaml
processors:
  transform:
    metric_statements:
      - context: datapoint
        statements:
          - set(attributes["rabbitmq.queue.name"], resource.attributes["rabbitmq.queue.name"])

service:
  pipelines:
    metrics:
      receivers: [rabbitmq]
      processors: [transform]
      exporters: [otlphttp]
```

Lift only `rabbitmq.queue.name`. The charts match each metric on its exact tag set, so lifting `rabbitmq.vhost.name` or `rabbitmq.node.name` as well stops them matching.

## RabbitMQ automated dashboard

The "RabbitMQ" dashboard is ordered by urgency of signal: dropped messages and backlog first, then consumer health, then throughput.

The following graphs are displayed in this automated dashboard:

- Messages dropped
- Messages ready
- Messages unacknowledged
- Consumers
- Message throughput (published, delivered and acknowledged)

These graphs display values from the `rabbitmq.*` metrics, broken down by queue.

This dashboard is currently marked Beta.
