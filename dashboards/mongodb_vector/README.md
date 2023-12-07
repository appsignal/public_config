# MongoDB dashboard (using Vector)

AppSignal tracks MongoDB metrics through its [Vector sink](https://docs.appsignal.com/vector.html).
When enabled, it shows a subset of the [metrics listed in Vector's documentation](https://vector.dev/docs/reference/configuration/sources/mongodb_metrics/) in three different dashboards:

- the **Status** dashboard, which shows more accessible metrics about the MongoDB instances:
  - **Memory usage** (`memory`): The memory usage of the MongoDB instance, by the kind of memory usage.
  - **Network usage** (`network_bytes_total`): The network usage of the MongoDB instance, incoming and outgoing.
  - **Document operations** (`mongod_metrics_document_total`): The amount of document operations performed on the MongoDB instance, by document operation type.
  - **Network connections** (`connections`): The amount of network connections open on the MongoDB instance, by their status.
  - **Transactions** (`mongod_wiredtiger_transactions_total`): The amount of transactions performed on the MongoDB instance, by their status or outcome.
  - **Open sessions** (`mongod_wiredtiger_session_open_sessions`): The amount of sessions opened on the MongoDB instance.
- the **WiredTiger** dashboard, which shows metrics about MongoDB's internal WiredTiger engine:
  - **Journal operations** count (`mongod_wiredtiger_log_operations_total`): the count of journal operations performed on the MongoDB instance, by type.
  - **Journal operations** in bytes (`mongod_wiredtiger_log_bytes_total`): the amount of payload received and bytes written in the MongoDB instance's journal.
  - **Cache size** (`mongod_wiredtiger_cache_bytes`): the amount of data stored in the MongoDB instance's cache, by the type or status of the cache node.
  - **Block manager** (`mongod_wiredtiger_blockmanager_bytes_total`): the amount of bytes read and written by the MongoDB instance's block manager.
  - **Concurrent transaction tickets** (`mongod_wiredtiger_concurrent_transactions_available_tickets`): the amount of available concurrent transaction tickets in the MongoDB instance, by type. If all concurrent transaction tickets are taken by transactions in progress, new transactions will be queued.
  - **Open cursor** (`mongod_metrics_cursor_open`): the amount of cursors open on the MongoDB instance, by state.
- the **Replication** dashboard, which shows metrics about the internal replication processes of the MongoDB cluster:
  - **Network replication** (`mongod_metrics_repl_network_bytes_total`): the amount of bytes read and written as part of the MongoDB cluster replication process.
  - **Replication buffer** (`mongod_metrics_repl_buffer_size_bytes`): the size in bytes of the buffered replication operations waiting to be transmitted to other members of the cluster.
  - **Replication executor queue** (`mongod_metrics_repl_executor_queue`): the size in bytes of the replication operations received from other clusters waiting to be applied, by operation type.
  - **Replication apply time** (`mongod_metrics_repl_apply_batches_seconds_total`): the amount of time, in seconds (rounded to the nearest second) spent applying replication operations.

All metrics are shown per host, meaning there's a line (or more) in each graph for each of the MongoDB instances connected to Vector.
