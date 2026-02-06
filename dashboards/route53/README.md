# AWS Route53 automated dashboard

[AWS Route53](https://aws.amazon.com/route53/) is a highly available and scalable Domain Name System (DNS) web service.
Route53 connects user requests to internet applications running on AWS or on-premises.

The following graphs are displayed in this automated dashboard:

## DNS Query Metrics

- [DNS Queries](#dns-queries)

## Health Check Metrics

- [Health Check Percentage Healthy](#health-check-percentage-healthy)
- [Health Check Status](#health-check-status)

---

## DNS Query Metrics

### DNS Queries

The "DNS Queries" graph shows the number of DNS queries that Route 53 responds to for all resource record sets in the hosted zone.

This graph displays values from the `aws_route53_dns_queries` metric.

Route 53 automatically sends DNS query metrics to CloudWatch for all public hosted zones.
There is no charge for DNS query metrics.

This metric helps you:
- Monitor DNS traffic patterns and trends
- Identify unusual spikes in DNS queries
- Plan capacity for your DNS infrastructure

---

## Health Check Metrics

### Health Check Percentage Healthy

The "Health Check Percentage Healthy" graph shows the percentage of Route 53 health checkers that consider the selected endpoint to be healthy.

This graph displays values from the `aws_route53_health_check_percentage_healthy` metric.

Route 53 health checkers are distributed around the world, and this metric aggregates their responses.
A value below 18% typically indicates an unhealthy endpoint.

### Health Check Status

The "Health Check Status" graph shows the status of the health check endpoint.

This graph displays values from the `aws_route53_health_check_status` metric.

The metric returns:
- 1 if the endpoint is healthy
- 0 if the endpoint is unhealthy

This binary metric is useful for:
- Creating CloudWatch alarms
- Triggering automated failover
- Monitoring endpoint availability
