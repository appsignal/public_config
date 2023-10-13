# PostgresQL Dashboard

AppSignal tracks PostgresQL metrics through its [Vector sink](https://docs.appsignal.com/vector.html).
When enabled, it shows a subset of the [metrics listed in Vector's documentation](https://vector.dev/docs/reference/configuration/sources/postgresql_metrics/):

- pg_stat_database_deadlocks_total
- pg_stat_database_numbackends
- pg_stat_database_temp_bytes_total
- pg_stat_database_temp_files_total
- pg_stat_database_tup_deleted_total
- pg_stat_database_tup_fetched_total
- pg_stat_database_tup_inserted_total
- pg_stat_database_tup_returned_total
- pg_stat_database_tup_updated_total
- pg_stat_database_xact_commit_total
- pg_stat_database_xact_rollback_total
