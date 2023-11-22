# Node.js automated dashboards

There are two automated dashboards for the AppSignal for Node.js integration:

- [Heap Statistics](#heap-statistics-automated-dashboard)
- [Postgres](#postgres-automated-dashboard-deprecated) (deprecated)

## Heap statistics automated dashboard

The following metrics are reported through this automated dashboard. The metrics originate from [the `getHeapStatistics()` method in the Node.js `v8` module](https://nodejs.org/api/v8.html#v8getheapstatistics), and they all refer to the internals of the V8 JavaScript engine which powers Node.js. All of them are gauges, tagged by the **hostname** of the machine:

- `nodejs_total_heap_size`: The total number of bytes that have been allocated in the heap.
- `nodejs_total_heap_size_executable`: The total number of bytes that have been allocated in the heap for executable code, such as bytecode and just-in-time compiled chunks.
- `nodejs_total_physical_size`: The number of bytes **committed** to the V8 JavaScript engine in the heap.
- `nodejs_used_heap_size`: The number of bytes that are used by application data.
- `nodejs_malloced_memory`: The current amount of memory allocated via `malloc`.
- `nodejs_number_of_native_contexts`: The number of top-level contexts currently active. For most applications, this value will always be `1`. A continuous increase in this value indicates a memory leak.
- `nodejs_number_of_detached_contexts`: The number of no longer active top-level contexts that have not yet been garbage-collected.

## Postgres automated dashboard (deprecated)

As of version 3.x of the AppSignal for Node.js integration, the metrics used on the Postgres automated dashboard are no longer emitted, and therefore this automated dashboard is no longer created.
