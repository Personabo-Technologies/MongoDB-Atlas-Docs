Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Host Metrics

Share Feedback

|  
  
|  
  
  * `ASSERT_REGULAR`

  * `ASSERT_WARNING`

  * `ASSERT_MSG`

  * `ASSERT_USER`

|

Measures the rate of asserts for a MongoDB process, as collected from the
MongoDB `serverStatus` command's `asserts` document.  
  
  * `BACKGROUND_FLUSH_AVG`

|

Amount of data flushed in the background.  
  
  * `CACHE_BYTES_READ_INTO`

  * `CACHE_BYTES_WRITTEN_FROM`

|

Applies to a MongoDB process's WiredTiger storage engine, as collected from
the MongoDB `serverStatus` command's `wiredTiger.cache` and
`wiredTiger.concurrentTransactions` documents.  
  
  * `CACHE_DIRTY_BYTES`

  * `CACHE_USED_BYTES`

|

Total dirty or used bytes cached in memory for serving reads and writes.  
  
  * `CONNECTIONS`

  * `SERVERLESS_CONNECTIONS`

  * `CONNECTIONS_PERCENT`

  * `SERVERLESS_CONNECTIONS_PERCENT`

|

Measures connections to a MongoDB process, as collected from the MongoDB
`serverStatus` command's `connections` document.  
  
  * `CURSORS_TOTAL_OPEN`

  * `CURSORS_TOTAL_TIMED_OUT`

  * `CURSORS_TOTAL_CLIENT_CURSORS_SIZE`

|

Measures the number of cursors for a MongoDB process, as collected from the
MongoDB `serverStatus` command's `metrics.cursor` document.  
  
  * `DB_DATA_SIZE_TOTAL`

  * `SERVERLESS_DATA_SIZE_TOTAL`

|

Amount of storage space in bytes that your stored data uses.  
  
  * `DB_STORAGE_TOTAL`

  * `DB_INDEX_SIZE_TOTAL`

|

Measures the database's on-disk storage space, as collected from the MongoDB
`dbStats` command.

## Note

Atlas retrieves database metrics every 20 minutes by default but adjusts
frequency when necessary to reduce the impact on database performance.  
  
  * `DB_DATA_SIZE_TOTAL_WO_SYSTEM`

|

Sum total size in bytes of the document data (including the padding factor)
across non-system databases.  
  
  * `LOGICAL_SIZE`

|

Logical size of cluster data.  
  
  * `DISK_PARTITION_SPACE_USED_DATA`

  * `DISK_PARTITION_SPACE_USED_INDEX`

  * `DISK_PARTITION_SPACE_USED_JOURNAL`

  * `DISK_PARTITION_UTILIZATION_DATA`

  * `DISK_PARTITION_UTILIZATION_INDEX`

  * `DISK_PARTITION_UTILIZATION_JOURNAL`

  * `DISK_PARTITION_READ_IOPS_DATA`

  * `DISK_PARTITION_READ_IOPS_INDEX`

  * `DISK_PARTITION_READ_IOPS_JOURNAL`

  * `DISK_PARTITION_WRITE_IOPS_DATA`

  * `DISK_PARTITION_WRITE_IOPS_INDEX`

  * `DISK_PARTITION_WRITE_IOPS_JOURNAL`

  * `DISK_PARTITION_READ_LATENCY_DATA`

  * `DISK_PARTITION_READ_LATENCY_INDEX`

  * `DISK_PARTITION_READ_LATENCY_JOURNAL`

  * `DISK_PARTITION_WRITE_LATENCY_DATA`

  * `DISK_PARTITION_WRITE_LATENCY_INDEX`

  * `DISK_PARTITION_WRITE_LATENCY_JOURNAL`

|

Partition measurements for different types of MongoDB data.  
  
  * `MAX_DISK_PARTITION_SPACE_USED_DATA`

  * `MAX_DISK_PARTITION_SPACE_USED_INDEX`

  * `MAX_DISK_PARTITION_SPACE_USED_JOURNAL`

  * `MAX_DISK_PARTITION_UTILIZATION_DATA`

  * `MAX_DISK_PARTITION_UTILIZATION_INDEX`

  * `MAX_DISK_PARTITION_UTILIZATION_JOURNAL`

  * `MAX_DISK_PARTITION_READ_IOPS_DATA`

  * `MAX_DISK_PARTITION_READ_IOPS_INDEX`

  * `MAX_DISK_PARTITION_READ_IOPS_JOURNAL`

  * `MAX_DISK_PARTITION_WRITE_IOPS_DATA`

  * `MAX_DISK_PARTITION_WRITE_IOPS_INDEX`

  * `MAX_DISK_PARTITION_WRITE_IOPS_JOURNAL`

  * `MAX_DISK_PARTITION_READ_LATENCY_DATA`

  * `MAX_DISK_PARTITION_READ_LATENCY_INDEX`

  * `MAX_DISK_PARTITION_READ_LATENCY_JOURNAL`

  * `MAX_DISK_PARTITION_WRITE_LATENCY_DATA`

  * `MAX_DISK_PARTITION_WRITE_LATENCY_INDEX`

  * `MAX_DISK_PARTITION_WRITE_LATENCY_JOURNAL`

|

Maximum values for partition measurements for different types of MongoDB data.  
  
  * `DISK_PARTITION_QUEUE_DEPTH_DATA`

  * `DISK_PARTITION_QUEUE_DEPTH_INDEX`

  * `DISK_PARTITION_QUEUE_DEPTH_JOURNAL`

|

Average length of the queue of requests issued to the disk partition that
MongoDB uses.  
  
  * `MAX_DISK_PARTITION_QUEUE_DEPTH_DATA`

  * `MAX_DISK_PARTITION_QUEUE_DEPTH_INDEX`

  * `MAX_DISK_PARTITION_QUEUE_DEPTH_JOURNAL`

|

Maximum disk queue depth values over the time period specified by the metric
granularity. Disk queue depth is the average length of the queue of requests
issued to the disk partition that MongoDB uses.  
  
  * `DOCUMENT_RETURNED`

  * `DOCUMENT_INSERTED`

  * `DOCUMENT_UPDATED`

  * `DOCUMENT_DELETED`

|

Average rate per second of documents returned, inserted, updated, or deleted
for a selected time period.  
  
  * `EXTRA_INFO_PAGE_FAULTS`

  * `GLOBAL_ACCESSES_NOT_IN_MEMORY`

  * `GLOBAL_PAGE_FAULT_EXCEPTIONS_THROWN`

|

Measurements on page faults related to the host.  
  
  * `FTS_MEMORY_RESIDENT`

  * `FTS_MEMORY_VIRTUAL`

  * `FTS_MEMORY_SHARED`

  * `FTS_CURRENT_MEMORY`

  * `FTS_MAX_MEMORY`

|

Memory usage for Atlas Search processes, in bytes.  
  
  * `FTS_PROCESS_CPU_USER`

  * `FTS_PROCESS_CPU_KERNEL`

  * `FTS_PROCESS_DISK`

  * `NORMALIZED_FTS_PROCESS_CPU_USER`

  * `NORMALIZED_FTS_PROCESS_CPU_KERNEL`

|

Percentage of CPU in use by Atlas Search processes.  
  
  * `GLOBAL_LOCK_CURRENT_QUEUE_TOTAL`

  * `GLOBAL_LOCK_CURRENT_QUEUE_READERS`

  * `GLOBAL_LOCK_CURRENT_QUEUE_WRITERS`

  * `GLOBAL_LOCK_PERCENTAGE`

|

Measures operations waiting on locks, as collected from the MongoDB
`serverStatus` command.  
  
  * `INDEX_COUNTERS_BTREE_ACCESSES`

  * `INDEX_COUNTERS_BTREE_HITS`

  * `INDEX_COUNTERS_BTREE_MISSES`

  * `INDEX_COUNTERS_BTREE_MISS_RATIO`

|

Measurements concerning B-tree index activity.  
  
  * `JOURNALING_COMMITS_IN_WRITE_LOCK`

  * `JOURNALING_MB`

  * `JOURNALING_WRITE_DATA_FILES_MB`

|

Measurements concerning journaling activity.  
  
  * `MEMORY_RESIDENT`

  * `MEMORY_VIRTUAL`

  * `MEMORY_MAPPED`

  * `COMPUTED_MEMORY`

|

Measures memory for a MongoDB process, as collected from the MongoDB
`serverStatus` command's `mem` document.  
  
  * `MUNIN_CPU_USER`

  * `MUNIN_CPU_NICE`

  * `MUNIN_CPU_SYSTEM`

  * `MUNIN_CPU_IOWAIT`

  * `MUNIN_CPU_IRQ`

  * `MUNIN_CPU_SOFTIRQ`

  * `MUNIN_CPU_STEAL`

|

Measurements concerning munin-node CPU activity.  
  
  * `NETWORK_BYTES_IN`

  * `NETWORK_BYTES_OUT`

  * `NETWORK_NUM_REQUESTS`

  * `SERVERLESS_NETWORK_BYTES_IN`

  * `SERVERLESS_NETWORK_BYTES_OUT`

  * `SERVERLESS_NETWORK_NUM_REQUESTS`

|

Measures throughput for MongoDB process, as collected from the MongoDB
`serverStatus` command's `network` document.  
  
  * `OPCOUNTER_CMD`

  * `OPCOUNTER_QUERY`

  * `OPCOUNTER_UPDATE`

  * `OPCOUNTER_DELETE`

  * `OPCOUNTER_GETMORE`

  * `OPCOUNTER_INSERT`

  * `SERVERLESS_OPCOUNTER_CMD`

  * `SERVERLESS_OPCOUNTER_QUERY`

  * `SERVERLESS_OPCOUNTER_UPDATE`

  * `SERVERLESS_OPCOUNTER_DELETE`

  * `SERVERLESS_OPCOUNTER_GETMORE`

  * `SERVERLESS_OPCOUNTER_INSERT`

|

Measures the rate of database operations on a MongoDB process since the
process last started, as collected from the MongoDB `serverStatus` command's
`opcounters` document.  
  
  * `OPCOUNTER_REPL_CMD`

  * `OPCOUNTER_REPL_UPDATE`

  * `OPCOUNTER_REPL_DELETE`

  * `OPCOUNTER_REPL_INSERT`

|

Measures the rate of database operations on MongoDB secondaries, as collected
from the MongoDB `serverStatus` command's `opcountersRepl` document.  
  
  * `OPERATIONS_SCAN_AND_ORDER`

|

For a selected time period, the average rate per second for operations that
perform a sort but cannot perform the sort using an index.  
  
  * `AVG_READ_EXECUTION_TIME`

  * `AVG_WRITE_EXECUTION_TIME`

  * `AVG_COMMAND_EXECUTION_TIME`

  * `SERVERLESS_AVG_READ_EXECUTION_TIME`

  * `SERVERLESS_AVG_WRITE_EXECUTION_TIME`

  * `SERVERLESS_AVG_COMMAND_EXECUTION_TIME`

|

The execution time in milliseconds per read, write, or command operation over
the selected time period.  
  
  * `OPLOG_MASTER_TIME`

  * `OPLOG_MASTER_TIME_ESTIMATED_TTL`

  * `OPLOG_SLAVE_LAG_MASTER_TIME`

  * `OPLOG_MASTER_LAG_TIME_DIFF`

  * `OPLOG_RATE_GB_PER_HOUR`

|

Measurements that apply to the MongoDB process's oplog.  
  
  * `QUERY_EXECUTOR_SCANNED`

|

Average rate per second to scan index items during queries and query-plan
evaluations. This rate is driven by the same value as `totalKeysExamined` in
the output of `explain`. This measurement is found on the host's `Query
Executor` chart, accessed when viewing metrics.  
  
  * `QUERY_EXECUTOR_SCANNED_OBJECTS`

|

Average rate per second to scan documents during queries and query-plan
evaluations. Atlas derives the rate using the `explain` output's
`totalDocsExamined` value. This measurement is found on the host's `Query
Executor` chart, accessed when viewing metrics.  
  
  * `QUERY_TARGETING_SCANNED_PER_RETURNED`

|

Ratio of the number of index items scanned to the number of documents
returned. This measurement is found on the host's `Query Targeting` chart,
accessed when viewing metrics.

## Note

The changestream cursors that the Atlas Search process (`mongot`) uses for
replication can contribute to the query targeting ratio and trigger query
targeting alerts if the ratio is high.  
  
  * `QUERY_TARGETING_SCANNED_OBJECTS_PER_RETURNED`

|

Ratio of the number of documents scanned to the number of documents returned.
This measurement is found on the host's `Query Targeting` chart, accessed when
viewing metrics.

## Note

The changestream cursors that the Atlas Search process (`mongot`) uses for
replication can contribute to the query targeting ratio and trigger query
targeting alerts if the ratio is high.  
  
  * `SEARCH_INDEX_SIZE`

|

Total size of all indexes on disk in bytes.  
  
  * `SEARCH_NUMBER_OF_FIELDS_IN_INDEX`

|

Total number of unique fields present in the Atlas Search index.  
  
  * `SEARCH_REPLICATION_LAG`

|

Approximate number of milliseconds that Atlas Search is behind in replicating
changes from the oplog of `mongod`.  
  
  * `SEARCH_OPCOUNTER_INSERT`

  * `SEARCH_OPCOUNTER_DELETE`

  * `SEARCH_OPCOUNTER_UPDATE`

  * `SEARCH_OPCOUNTER_GETMORE`

|

Total number of Atlas Search operations.  
  
  * `SEARCH_NUMBER_OF_QUERIES_TOTAL`

  * `SEARCH_NUMBER_OF_QUERIES_ERROR`

  * `SEARCH_NUMBER_OF_QUERIES_SUCCESS`

|

Total number of Atlas Search queries with each status.  
  
  * `SERVERLESS_TOTAL_READ_UNITS`

|

Total serverless Read Processing Units (RPUs).  
  
  * `SWAP_USAGE_USED`

  * `SWAP_USAGE_FREE`

  * `MAX_SWAP_USAGE_USED`

  * `MAX_SWAP_USAGE_FREE`

|

Swap space used and available, measured in bytes.  
  
  * `SYSTEM_MEMORY_USED`

  * `SYSTEM_MEMORY_FREE`

  * `SYSTEM_MEMORY_PERCENT_USED`

|

Number of bytes of physical memory in use and available to the system.  
  
  * `MAX_SYSTEM_MEMORY_USED`

  * `MAX_SYSTEM_MEMORY_FREE`

  * `MAX_SYSTEM_MEMORY_PERCENT_USED`

|

Maximum system memory values in bytes.  
  
  * `SYSTEM_MEMORY_AVAILABLE`

  * `MAX_SYSTEM_MEMORY_AVAILABLE`

|

Estimate of the number of bytes of system memory available for running new
applications, without swapping.  
  
  * `SYSTEM_NETWORK_IN`

  * `SYSTEM_NETWORK_OUT`

|

Average rate of physical bytes received and transmitted per second by the
`eth0` network interface.  
  
  * `MAX_SYSTEM_NETWORK_IN`

  * `MAX_SYSTEM_NETWORK_OUT`

|

Maximum values for the average rate of physical bytes (after any wire
compression) sent to or from this database server per second over the selected
sample period.  
  
  * `TICKETS_AVAILABLE_READS`

  * `TICKETS_AVAILABLE_WRITES`

|

Measurement of the WiredTiger storage engine `wiredTiger.cache` and
`wiredTiger.concurrentTransactions` documents as collected from the MongoDB
`serverStatus` command.  
  
  * `NORMALIZED_SYSTEM_CPU_USER`

  * `NORMALIZED_SYSTEM_CPU_STEAL`

|

CPU usage of processes on the host server, scaled to a range of 0-100% by
dividing by the number of CPU cores.  
  
  * `MAX_NORMALIZED_SYSTEM_CPU_USER`

  * `MAX_NOMRALIZED_SYSTEM_CPU_STEAL`

|

Maximum CPU usage values of all processes on the node, scaled to a range of
0-100% by dividing by the number of CPU cores.  
  
← Oplog AccessSupported Browsers →

