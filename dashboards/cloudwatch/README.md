# AWS CloudWatch automated dashboard

[AWS CloudWatch Metric Streams](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatchMetrics.html) enables you to stream CloudWatch metrics to other AWS services or third-party services in near real-time.

The following graphs are displayed in this automated dashboard:

- [MetricUpdate vs TotalMetricUpdate](#metricupdate-vs-totalmetricupdate)
- [PublishErrorRate](#publisherrorrate)

## MetricUpdate vs TotalMetricUpdate

The "MetricUpdate vs TotalMetricUpdate" graph shows the volume of metric updates being processed by your CloudWatch Metric Streams.

The **MetricUpdate** metric represents the number of metric updates sent to the metric stream, while the **TotalMetricUpdate** metric includes both the MetricUpdate count and additional statistics that are being streamed.

This graph displays values from the following metrics:
- `cloudwatch_metricstreams_metric_update` - Raw metric update count
- `cloudwatch_metricstreams_total_metric_update` - Total metric update count including additional statistics

This graph will show a line for each metric name, allowing you to compare the volume of metric updates against the total processing volume.

## PublishErrorRate

The "PublishErrorRate" graph shows the number of unrecoverable errors that occur when CloudWatch attempts to put data into the Firehose delivery stream.

This metric is critical for monitoring the health of your Metric Streams configuration, as errors indicate problems with data delivery to downstream services.

This graph displays values from the `cloudwatch_metricstreams_publish_error_rate` metric, which counts unrecoverable errors during the publishing process.

An increase in this metric may indicate:
- Configuration issues with the Firehose delivery stream
- Permission problems
- Network connectivity issues
- Service limits being reached

This graph will show a line for the error rate metric, allowing you to quickly identify and troubleshoot delivery issues.
