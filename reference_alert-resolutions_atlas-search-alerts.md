Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Fix Atlas Search Issues

Share Feedback

On this page

  * Alert Conditions
  * Common Triggers
  * Fix the Immediate Problem
  * Implement a Long-Term Solution
  * Monitor Your Progress

Atlas Search triggers Atlas Search alerts when the amount of CPU and memory
used by Atlas Search processes reaches a specified threshold. If the search
process (`mongot`) runs out of memory, indexing and queries fail. You can
configure Atlas Search alert conditions in the project alert settings modal.
You can also view Atlas Search metrics with cluster monitoring.

## Note

If you run `sh.shardCollection()` on an unsharded collection with Atlas Search
indexes, the Atlas Search indexes might enter an invalid state after sharding.
To mitigate this issue, you can create a new index on the collection after
sharding, or contact support to restart the `mongot` processes on the nodes.

## Alert Conditions

You can configure the following alert conditions in the project-level alert
settings page to trigger alerts.

`Atlas Search: Index Replication Lag` occurs if the approximate number of
milliseconds that Atlas Search is behind in replicating changes from the oplog
of `mongod` is above or below the threshold.

`Atlas Search: Index Size on Disk` occurs if the total size of all Atlas
Search indexes on disk in bytes is above or below the threshold.

`Atlas Search: Max Number of Lucene Docs` occurs if the upper bound number of
Lucene docs used to store Atlas Search indexes for a given replica set or
shard is above the threshold.

`Atlas Search: Number of Error Queries` occurs if the number of queries for
which Atlas Search is unable to return a response is above or below the
threshold.

`Atlas Search: Number of Index Fields` occurs if the total number of unique
fields present in the Atlas Search index is above or below the threshold.

`Atlas Search: Number of Successful Queries` occurs if the number of queries
for which Atlas Search successfully returned a response is above or below the
threshold.

`Atlas Search: Total Number of Queries` occurs if the number of queries
submitted to Atlas Search is above or below the threshold.

`Atlas Search Opcounter: Delete` occurs if the total number of documents or
fields (specified in the index definition) removed per second is above or
below the threshold.

`Atlas Search Opcounter: Getmore` occurs if the total number of `getmore`
commands run on all Atlas Search queries per second is above or below the
threshold.

`Atlas Search Opcounter: Insert` occurs if the total number of documents or
fields (specified in the index definition) that Atlas Search indexes per
second is above or below the threshold.

`Atlas Search Opcounter: Update` occurs if the total number of documents or
fields (specified in the index definition) that Atlas Search updates per
second is above or below the threshold.

`Insufficient disk space to support rebuilding search indexes` occurs if your
database deployment runs out of enough free disk space to support your Atlas
Search indexes.

## Note

This alert might appear when Atlas automatically upgrades your search indexes
to enable new features. Your database deployment must have sufficient disk
space for both the previous and new version of the index. After the index
upgrade completes, Atlas deletes the old version of the index, which frees up
disk space.

`Search Memory: Resident` occurs if the total bytes of resident memory
occupied by the Atlas Search process is above or below the threshold.

`Search Memory: Shared` occurs if the total bytes of shared memory occupied by
the Atlas Search process is above or below the threshold.

`Search Memory: Virtual` occurs if the total bytes of virtual memory occupied
by the Atlas Search process is above or below the threshold.

`Search Process: CPU (Kernel) %` occurs if the percentage of time the CPU
spent servicing operating system calls for the Atlas Search process is above
the threshold.

`Search Process: CPU (User) %` occurs if the percentage of time the CPU spent
servicing the Atlas Search process is above the threshold.

`Search Process: Disk space used` occurs if the total bytes of disk space used
by the Atlas Search process is above the threshold.

`Search Process: Ran out of memory` occurs if the search process (`mongot`)
runs out of memory. If the search process runs out of memory, indexing and
queries fail.

## Note

The `Search Process: Ran out of memory` alert runs automatically by default.
You can configure the alert setting to disable this notification.

## Common Triggers

Atlas Search alerts often occur when you try to build a large or complex
search index. These indexes remain in the Initial Sync phase until you resolve
the memory issue.

## Fix the Immediate Problem

If the search process (`mongot`) runs out of memory or disk space, you can
upgrade your cluster to fix the immediate problem. You can select a cluster
tier with more memory, storage, and IOPS.

## Implement a Long-Term Solution

To prevent Atlas Search alerts in the future, carefully review the Tune Atlas
Search Performance for Atlas Search. Work to optimize your indexes.

## Monitor Your Progress

View the available Atlas Search charts to monitor Atlas Search metrics.

Monitor Atlas Search metrics to evaluate and optimize your Atlas Search
indexes.

To learn more, see View Cluster Metrics

← Atlas Search Query PerformanceReview Atlas Search Metrics →

