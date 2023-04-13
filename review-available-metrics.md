Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review Available Metrics

Share Feedback

You can review the following metrics to monitor your database deployments. All
hardware metrics include metrics or individual charts for maximum values.

## Important

The metrics available depend on your user role and database deployment type.

## Note

Currently, serverless instance metrics don't support any third-party services
(for example, Datadog).

Metric

|

Description  
  
|  
  
Asserts

|

Displays the following information:

  * ASSERT_REGULAR displays the average rate of regular asserts raised per second over the selected sample period.

  * ASSERT_WARNING displays the average rate of warnings per second over the selected sample period.

  * ASSERT_MSG displays the average rate of message asserts per second over the selected sample period. These internal server errors have a well-defined text string. Atlas logs stack traces for these.

  * ASSERT_USER displays the average rate of user asserts per second over the selected sample period. This metric includes asserts that a user generates, such as out of disk space or duplicate key errors.

Monitor asserts to track how many errors occur while trying to read or write
data. Check the server logs to identify the source of any errors.  
  
Avg Object Size

|

Displays the average object size across all collections in the database.

Monitor object size to track the size of your objects and better understand
your database space.  
  
Cache Activity

|

Displays the following information:

  * readInto (replica set) or cache read into (sharded cluster) displays the rate in bytes per second of data read from disk into memory to service queries.

  * writtenFrom (replica set) or cache written from (sharded cluster) displays the rate in bytes per second of data written from memory into disk to service writes.

Monitor the MongDB cache, which stores frequently accessed data in memory to
service queries faster.  
  
Cache Usage

|

Displays the following information:

  * dirty (replica set) or cache dirty (sharded cluster) displays the total dirty bytes cached in memory for serving reads and writes.

  * used (replica set) or cache used (sharded cluster) displays the total bytes cached in memory for serving reads and writes.

These metrics include both indexes and data from the working set.

Sustained high cache usage indicates the RAM is too small for your workloads.
Optimize your queries to avoid frequent disk reads. If write operations make
cache usage high, throttle them.  
  
Collections

|

Displays the number of collections in the database.

Monitor collections to determine restart times, continuous backup performance,
and stability.  
  
Connections (serverless instance/replica set) or connection (sharded cluster)

|

Displays the total number of active connections to the database deployment.

Monitor connections to determine whether the current connection limits are
sufficient. If necessary, upgrade the cluster tier.  
  
Cursors

|

Displays the following information:

  * totalOpen displays the number of cursors that the server maintains for clients.

  * totalTimedOut displays the average rate of cursors that have timed out per second over the selected sample period.

Monitor cursors to close unnecessary cursors and reduce the timeout
configuration in the application.  
  
DB Storage

|

Displays the following information:

  * storageSize (replica set) or db storage size (sharded cluster) displays the sum total amount of on-disk storage space allocated for document storage across all databases.

  * Data Size (serverless instance), dataSize (replica set), or db data size (sharded cluster) displays the amount of storage space in bytes that your stored data uses.

  * db data size without system displays the sum total size in bytes of the document data (including the padding factor) across non-system databases.

Atlas retrieves database metrics every 20 minutes by default but adjusts
frequency when necessary to reduce the impact on database performance.

Monitor storage space to determine whether to use disk auto-scaling or
manually increase the disk size. You can also monitor this metric to verify
backup billing.  
  
Disk IOPS

|

Displays input operations per second.

Monitor whether disk IOPS approaches the maximum provisioned IOPS. Determine
whether the cluster can handle future workloads.  
  
Disk Latency

|

Displays the following information:

  * Read displays the average amount of time to read from disk.

  * Write displays the average amount of time to write to disk.

Monitor disk latency to track the efficiency of reading from and writing to
disk.  
  
Disk Queue Depth

|

Displays the average length of the queue of requests issued to the disk
partition that MongoDB uses.

Monitor disk queue depth to identify potential issues and bottlenecks.  
  
Disk Space Free

|

Displays the total amount of free space remaining on disk.

Monitor free disk space to determine whether to use disk auto-scaling or
manually increase the disk size.  
  
Disk Space Percent Free

|

Displays the total amount of free space remaining on disk as a percentage of
the total disk space.

Monitor the percentage of free disk space to determine whether to use disk
auto-scaling or manually increase the disk size.  
  
Disk Space Used

|

Displays the total space on disk used.

Monitor the used disk space to determine whether to use disk auto-scaling or
manually increase the disk size.  
  
Document Metrics

|

Displays the following information:

  * Returned displays the documents per second returned.

  * Inserted displays the documents per second inserted.

  * Updated displays the documents per second updated.

  * Deleted displays the documents per second deleted.

Monitor document metrics to measure the work MongoDB completes.  
  
Execution Time

|

Displays the average time in seconds for the following metrics:

  * Average read operational latency

  * Average write operational latency

  * Average command operational latency

Monitor execution time for an increase in read operations to optimize queries
and indexes.  
  
Index Size

|

Displays the total size of all indexes in the database. This metric includes
the overhead incurred by indexes on top of the actual document data on which
the indexes are based.

Monitor the index size to manage your indexes. To learn more, see Indexing
Strategies.  
  
Indexes

|

Displays the total number of indexes in the database.

Monitor indexes to manage them. To learn more, see Indexing Strategies.  
  
Locks

|

Displays the following information:

  * GLOBAL_LOCK_CURRENT_QUEUE_TOTAL displays the number of operations queued waiting for any lock.

  * GLOBAL_LOCK_CURRENT_QUEUE_READERS displays the number of operations queued waiting for a read lock.

  * GLOBAL_LOCK_CURRENT_QUEUE_WRITERS displays the number of operations waiting for a write lock.

Monitor locks to optimize queries.  
  
Max Disk IOPS

|

Displays the following maximum disk IOPS values over the time period specified
by the metric granularity:

  * max read iops maximum disk read input operations per second.

  * max write iops maximum disk write input operations per second.

Monitor whether disk IOPS approaches the maximum provisioned IOPS. Determine
whether the cluster can handle future workloads.  
  
Max Disk Queue Depth

|

Displays the maximum disk queue depth values over the time period specified by
the metric granularity. Disk queue depth is the average length of the queue of
requests issued to the disk partition that MongoDB uses.

Monitor disk queue depth to identify potential issues and bottlenecks.  
  
Max Normalized System CPU

|

Displays the maximum CPU usage values of all processes on the node, scaled to
a range of 0-100% by dividing by the number of CPU cores.

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.  
  
Max Process CPU

|

Displays the following maximum process CPU values over the time period
specified by the metric granularity:

  * max user displays the maximum percentage of time that the CPU spent servicing the MongoDB process.

  * max kernel displays the maximum percentage of time the CPU spent servicing operating system calls for the MongoDB process.

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.  
  
Max System CPU

|

Displays the maximum CPU usage values of all processes on the node.

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.  
  
Max System Memory

|

Displays the maximum system memory values in bytes.

Monitor memory to determine whether to upgrade to a higher cluster tier.  
  
Memory

|

Displays the total consumption of memory in megabytes at a particular point in
time:

  * memory_resident (replica set) or memory resident (sharded cluster) displays the memory that the MongoDB process running on a node consumes. This metric excludes the consumption of other processes and does not represent the total memory that the node consumes.

  * memory_virtual (replica set) or memory virtual (sharded cluster) displays the memory reserved in disk to act as swap space.

Monitor memory to determine whether to upgrade to a higher cluster tier.  
  
Network

|

Displays the following information:

  * bytesIn displays the average rate of physical bytes (after any wire compression) sent to this database server per second over the selected sample period.

  * bytesOut displays the average rate of physical bytes (after any wire compression) sent from this database server per second over the selected sample period.

  * numRequests displays the average rate of requests sent to this database server per second over the selected sample period.

Monitor network metrics to track network performance.

  
  
Normalized Process CPU

|

Displays the following information:

  * user displays the percentage of time that the CPU spent servicing the MongoDB process, scaled to a range of 0-100% by dividing by the number of CPU cores.

  * kernel displays the percentage of time the CPU spent servicing operating system calls for the MongoDB process, scaled to a range of 0-100% by dividing by the number of CPU cores.

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.  
  
Normalized System CPU

|

Displays the CPU usage of all processes on the node, scaled to a range of
0-100% by dividing by the number of CPU cores.

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.  
  
Objects

|

Displays the number of objects in the database.

Monitor this metric to better understand your database space.  
  
OpCounters

|

Displays the number of the following operations per second run on a MongoDB
process since the process last started:

  * command (replica set) or cmd (sharded cluster)

  * query

  * insert

  * delete

  * update

  * getmore

Monitor MongoDB operations to validate performance issues related to high
workloads. Confirm the type of operations responsible for the load.  
  
OpCounters - Repl

|

Displays the following information:

  * command displays the average rate of replicated commands applied per second over the selected sample period.

  * insert displays the average rate of replicated inserts applied per second over the selected sample period.

  * delete displays the average rate of replicated deletes applied per second over the selected sample period.

  * update displays the average rate of replicated updates applied per second over the selected sample period.

Monitor MongoDB operations to validate performance issues related to high
workloads. Confirm the type of operations responsible for the load.  
  
Operation Execution Time

|

Displays the average time in milliseconds to execute the following operations:

  * avg ms/read (replica set) or execution time reads (sharded cluster)

  * avg ms/write (replica set) or execution time writes (sharded cluster)

  * avg ms/command (replica set) or execution time commands (sharded cluster)

Monitor execution time for an increase in read operations to optimize queries
and indexes. Determine whether you need to upgrade your cluster tier.  
  
Oplog GB/Hour

|

Displays the average rate in gigabytes of oplog data that the primary
generates per hour.

Monitor oplog data to determine whether you have to increase the oplog size.  
  
Page Faults

|

Displays the average rate of page faults on this process per second over the
selected sample period. In non-Windows environments this applies to hard page
faults only.

Monitor page faults to determine whether to increase your memory.  
  
Process CPU

|

Displays the following information:

  * user displays the percentage of time that the CPU spent servicing the MongoDB process.

  * kernel displays the percentage of time the CPU spent servicing operating system calls for the MongoDB process.

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.  
  
Query Executor

|

Displays the following information:

  * Index Items Scanned displays the number of index items scanned per second.

  * Documents Scanned displays the number of documents scanned per second.

Monitor the query executor to determine whether you have any inefficient
queries.  
  
Query Targeting

|

Displays the efficiency of read operations run on MongoDB:

  * Scanned Objects to Returned (replica set) or scanned objects / returned (sharded cluster) displays the number of documents scanned to return one document.

  * Scanned Keys to Returned (replica set) or scanned keys / returned (sharded cluster) displays the number of index keys scanned to return one document.

Monitor query targeting to determine read efficiency and optimize queries and
indexes.

## Note

The changestream cursors that the Atlas Search process (`mongot`) uses for
replication can contribute to the query targeting ratio and trigger query
targeting alerts if the ratio is high.  
  
Read/Write Units

|

Displays the following information:

  * Total Read Processing Units (RPUs)

  * Total Write Processing Units (WPUs)

Monitor read and write units to help optimize queries and indexes.  
  
Replication Headroom

|

Displays the difference between the primary's replication oplog window and the
secondary's replication lag.

Monitor replication headroom to determine whether the secondary might fall off
the oplog.  
  
Replication Lag

|

Displays the approximate number of seconds the secondary is behind the primary
in write application.

Monitor replication lag to determine whether the secondary might fall off the
oplog.  
  
Replication Oplog Window

|

Displays the estimated average number of hours of database operations
available in the primary's replication oplog, based on oplog churn. If
replication lag on a secondary node exceeds the replication oplog window, and
replication headroom reaches zero, a full resync is required for that node to
become healthy again.

Monitor the replication oplog window, together with replication headroom, to
determine whether the secondary may soon require a full resync. The
replication oplog window often helps to determine in advance the resilience of
secondaries to planned and unplanned outages.  
  
Scan and Order

|

Displays the number of operations per second returning results that required a
sort in-memory.

Monitor this metric to identify whether your queries need indexes.  
  
Shard Data Size

|

Displays the amount of storage space in bytes that your stored data uses on
each shard. You can access this chart only for sharded clusters with MongoDB
6.0+.

Monitor this metric to verify whether you have balanced shards.  
  
Shard Document Count

|

Displays the number of documents on each shard. You can access this chart only
for sharded clusters with MongoDB 6.0+.

Monitor this metric to verify whether you have balanced shards.  
  
System CPU

|

Displays the CPU usage of all processes on the node.

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.  
  
System Memory

|

Displays the following information:

  * used displays the number of bytes of physical memory in use.

  * available displays an estimate of the number of bytes of system memory available for running new applications, without swapping.

Monitor memory to determine whether to upgrade to a higher cluster tier.  
  
Tickets Available

|

Displays the following information:

  * Tickets Available Read displays the number of read tickets available to the WiredTiger storage engine. Read tickets represent the number of concurrent read operations allowed into the storage engine. When this value reaches zero, new read requests might queue until a read ticket becomes available.

  * Tickets Available Write displays the number of write tickets available to the WiredTiger storage engine. Write tickets represent the number of concurrent write operations allowed into the storage engine. When this value reaches zero, new write requests might queue until a write ticket becomes available.

Monitor the tickets available to see when read and write requests queue.  
  
Disk Util %

|

Displays the percentage of time that requests are issued to and serviced by
disk, _not_ the IOPS capacity utilization. For example, if during a given
period there is at least one ongoing operation on the disk, then the disk
utilization is 100%. This does not mean that the disk has reached the storage
limit in throughput or IOPS.

This metric includes requests from any process, not just MongoDB processes.

Monitor whether utilization is high. Determine whether to increase the
provisioned IOPS or upgrade the cluster.  
  
Views

|

Displays the number of views in the database.

Monitor views to help optimize your database.  
  
← Review Atlas Search MetricsIntegrate with Third-Party Services →

