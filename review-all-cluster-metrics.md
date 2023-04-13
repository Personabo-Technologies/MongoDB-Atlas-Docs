Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review Project Overview

Share Feedback

Atlas CLI

Atlas UI

You can view select project metrics using the Atlas CLI.

## View Disk Metrics

To return the metrics for a disk partition on a specified host using the Atlas
CLI, run the following command:

    
    
    atlas metrics disks describe <hostname:port> <diskName> [options]  
      
  
To list available disks or disk partitions on a specified host using the Atlas
CLI, run the following command:

    
    
    atlas metrics disks list <hostname:port> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas metrics disks describe and atlas metrics
disks list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

Monitor database deployment metrics to identify performance issues and
determine whether your current database deployment meets your requirements.
For more information on the metrics available to monitor your database
deployments, see Review Available Metrics.

## Available Charts

Atlas displays up to four of the following charts for each database deployment
in the project:

## Note

Currently, serverless instance metrics don't support any third-party services
(for example, Datadog).

## Note

### Monitoring Data Storage Granularity

Atlas stores metrics data at increasing granularity levels. For more
information, see Monitoring Data Storage Granularity.

Chart

|

Data

|

Use Case  
  
||  
  
Connections

|

The total number of active connections to the database deployment

For a replica set, the chart shows the number of active connections to the
primary.

For a sharded cluster, the chart shows the sum of all active connections to
each primary in the cluster.

|

Monitor connections to determine whether the current connection limits are
sufficient. If necessary, upgrade the cluster tier.  
  
Data Size

 _Serverless Instances Only_

|

Displays the amount of storage space in bytes that your stored data uses.

|

Monitor storage space to determine whether to use disk auto-scaling or
manually increase the disk size. You can also monitor this metric to verify
backup billing.  
  
Disk IOPS

`M10+` _Clusters Only_

|

The sum of read and write input/output operations per second (IOPS) for the
cluster.

|

Monitor whether disk IOPS approaches the maximum provisioned IOPS. Determine
whether the cluster can handle future workloads.  
  
Disk Latency 1

|

The latency, in milliseconds, of the disk partition used by MongoDB.

|

Monitor Disk Latency to determine the average amount of time to read from or
write to disk.  
  
Disk Usage

 _Serverless Instances and_ `M10+` _Clusters Only_

|

The total bytes of used disk space for the database deployment.

For a replica set, the chart shows the disk usage of the primary host machine.

For a sharded cluster, the chart shows the sum of disk usage on each primary
host in the cluster.

The line graph is green for less than 75% disk usage, yellow for 75%-89% disk
usage, and red for 90% or more disk usage.

|

Monitor the combined size of your data and MongoDB operational data (buffer,
journal, and log files) on the cluster.  
  
Logical Size

`M0/M2/M5` _Clusters Only_

|

Displays the sum of total bytes of the documents and index data across all
databases in the database deployment.

The line graph is green for less than 75% of the max storage size, yellow for
75%-89% of the max storage size, and red for 90% or more of the max storage
size.

|

Monitor the size of the documents and index data on the database deployment.  
  
Network

 _Serverless Instances and_ `M0/M2/M5` _Clusters Only_

|

Displays the average rate of physical bytes or requests sent to/from this
database server per second over the selected sample period.

|

Monitor network metrics to track network performance.  
  
Operations

|

Displays the aggregated read (R) and write (W) operations on the database
deployment.

For a replica set, the chart shows operations for the primary.

For a sharded cluster, the chart shows the sum of the operations on each
primary in the cluster.

|

Monitor performance issues related to high workloads.  
  
Total Index Size

`M10+` _Clusters Only_

|

The total bytes of disk space used by indexes for every database in the
cluster.

|

Monitor the size of all indexes on your cluster.  
  
Util % 1

|

The percentage of time during which the partition is receiving and servicing
requests. This metric includes requests from all processes, not just MongoDB
processes.

|

Monitor whether utilization is high. Determine whether to increase the
provisioned IOPS or upgrade the cluster.  
  
1 Clusters which use NVMe SSDs for storage display `Disk Latency` and `Disk
Util %` charts using the maximum value across the physical drives that make up
the RAID. The following cluster tiers display RAID-based metrics if they use
NVMe:

  * `M80`

  * `M200`

  * `M400`

← Review Database Deployment MetricsReview Serverless Metrics →

