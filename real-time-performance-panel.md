Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Monitor Real-Time Performance

Share Feedback

On this page

  * Enable or Disable the Real-Time Performance Panel
  * Access the Real-Time Performance Panel
  * Graph View
  * Table View

 _Only available on M10+ clusters_

The Real-Time Performance Panel (RTPP) monitors and displays current network
traffic, database operations on the machines hosting MongoDB in your clusters,
and hardware statistics about the hosts. Use RTPP to visually identify
relevant database operations, evaluate query execution times and the ratio of
documents scanned to documents returned, monitor network load and throughput,
and discover potential replication lag on secondary members of replica sets.

## Enable or Disable the Real-Time Performance Panel

## Important

### Required Privileges

To enable or disable Real-Time Performance Panel for a project, you must have
the `Project Owner` role for the project.

Real-Time Performance Panel is enabled by default. To disable or enable the
Real-Time Performance Panel for a project:

1

### Click Settings.

2

### Toggle the button next to Real-Time Performance Panel.

## Access the Real-Time Performance Panel

To view the Real-Time Performance Panel:

1

### Click Database.

2

### Click the cluster whose current operations you want to evaluate.

If the replica set resides in a sharded cluster, first click the sharded
cluster containing the replica set.

3

### Click the member of the replica set that you want to view.

4

### Click Real Time.

Atlas displays the data as a graph. Click Table to view the data as a table.

5

### (Optional) Click Pause to stop RTPP from displaying incoming data. Click
Play to resume.

## Graph View

Chart/Location

|

Description  
  
|  
  
Connections, Network In, Network Out (Top of panel)

|

Displays the number of current connections to the machine hosting MongoDB and
the number of inbound and outbound bytes as reported by `mongostat`.  
  
CPU, Disk Util, and Sys Mem (Top of panel)

|

Displays the currently used percentage of CPU and disk capacity and the total
physical memory usage, excluding buffers and swap space, of the machine
hosting MongoDB.  
  
Operations

|

Displays the number of operations as reported by `mongostat`.  
  
Query Execution Times

|

Displays latency statistics for current read requests, write requests, and
other database commands. Available in MongoDB 3.6 or later. See `opLatencies`
at serverStatus for more information.  
  
Query Targeting

|

Displays the ratio of documents and objects scanned to documents and objects
returned in current queries. These statistics are useful in determining if and
how a query uses an index. See Analyze Query Performance for more information.

## Note

The changestream cursors that the Atlas Search process (`mongot`) uses for
replication can contribute to the query targeting ratio and trigger query
targeting alerts if the ratio is high.  
  
Reads & Writes

|

Displays the number of active reads, queued reads, active writes, and queued
writes as reported by `mongostat`.  
  
Replication Lag

|

Available only for secondary members of a replica set. Displays the time
required to replicate operations from the primary to the secondary members of
a replica set. See Replica Set Secondary Members for more information.  
  
Hottest Collections

|

Displays the collections with the most operations as reported by `mongotop`.
For each hot collection, the table also displays the Utilization Percent for
the collection.

Utilization Percent is calculated from the read and write times as reported by
`mongotop` during a sample period. Specifically, the Utilization Percent is
the percentage (rounded to the nearest 0.1%) of the read and write times for a
collection relative to the read and write times for all collections in the
deployment during the sample period. If no read and write operation occur
during this period, the Utilization Percent will be 0%.

The hottest collections correspond to the most current time displayed in the
charts. That is, if the display is running (i.e. not paused), the collections
correspond to the hottest collections at the current timestamp. If the display
is paused, the collections correspond to the hottest collections at the paused
time.  
  
Slowest Operations

|

Displays the slowest operations as reported by db.currentOp().

The operations correspond to the most current time displayed in the charts.
That is, if the display is running (i.e. not paused), the operations
correspond to the slowest operations at the current timestamp. If the display
is paused, the operations correspond to the slowest operations at the paused
time.

Select one of the operations to open the Operation Details panel, where you
can terminate the selected operation using the Kill Op button. The Kill Op
button issues the db.killOp() method on the selected operation.  
  
### Read Exact Metrics from Graph View

If you pause the Graph view of the Real-Time Performance Panel, you can hover
over a line graph to see its exact value, along with the slowest operations
and hottest collections, at a given moment in time.

Pausing the Performance Panel does not affect the collection of the underlying
data. When you resume the Graph view, the line graphs restart from an empty
display.

## Table View

Click __to hide or display fields from the table.

Fields

|

Description  
  
|  
  
Commands

Queries

Updates

Deletes

Inserts

GetMores

|

Displays the number of the specified operations (commands, queries, etc.) as
reported by `mongostat`.  
  
Time / Read

Time / Write

Time / Command

|

Displays latency statistics for current read requests, write requests, and
other database commands. To learn more, see `opLatencies` in serverStatus.  
  
Scanned / Returned

Scanned Objects / Returned

|

Displays the ratio of documents and objects scanned to documents and objects
returned in current queries. These statistics are useful in determining if and
how a query uses an index. To learn more, see Analyze Query Performance.  
  
Active Readers

Active Writers

Queued Readers

Queued Writers

|

Displays the number of active reads, queued reads, active writes, and queued
writes as reported by `mongostat`.  
  
Lag Time

|

Available only for secondary members of a replica set. Displays the time
required to replicate operations from the primary to the secondary members of
a replica set. To learn more, see Replica Set Secondary Members.  
  
CPU

Disk Util

Sys Mem

|

Displays the currently used percentage of CPU and disk capacity and the total
physical memory usage, excluding buffers and swap space, of the machine
hosting MongoDB.  
  
Connections

Bytes In

Bytes Out

|

Displays the number of current connections to the machine hosting MongoDB and
the number of inbound and outbound bytes as reported by `mongostat`.  
  
← Monitor Query PerformanceUpdate $text Queries with Atlas Search for Improved
Search Performance →

