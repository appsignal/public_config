# Process memory magic dashboard

The AppSignal tracks memory usage metrics about the process that it was started by, the app that's being monitored.

This graph may help determine a memory leak by showing a constant increase of the app process's memory over time, which would fall back to normal levels upon reboot or a deploy.

This graph displays values from the `process_rss` metric. This graph will show a line for each combination of values of the following metric tags:

- The `hostname` of the machine that emitted the metric.
- The `process_name`: the self defined name of the app process.
