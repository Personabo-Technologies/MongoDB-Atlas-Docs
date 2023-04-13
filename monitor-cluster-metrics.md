Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review Database Deployment Metrics

Share Feedback

On this page

  * View Metrics
  * Important Metrics
  * Monitoring Data Storage Granularity
  * Free Cluster and Shared Cluster Monitoring Considerations
  * Serverless Instance Monitoring Considerations

Atlas collects and displays metrics for your servers, databases, and MongoDB
processes.

Monitor database deployment metrics to identify performance issues and
determine whether your current database deployment meets your requirements.
For more information on the metrics available to monitor your database
deployments, see Review Available Metrics.

## Note

The number of servers that Atlas displays on the Metrics page at any given
time depends on the browser screen size. Use the Toggle Members section to
control which servers Atlas displays. Hover over the `S` and `P` icons to find
out which servers they represent.

## View Metrics

View Project Overview

    The Overview tab displays all the database deployments in an Atlas project and features core metrics per database deployment.
View Atlas Serverless Instance Metrics

    View the metrics for a specific serverless instance in an Atlas project.
View Atlas Replica Set Metrics

    View the metrics for a specific replica set in an Atlas project.
View Atlas Sharded Cluster Metrics

    View the metrics for a specific sharded cluster in an Atlas project.
View MongoDB Processes

    View the metrics for a specific MongoDB process in an Atlas cluster.
View Real-Time Performance Metrics

    View real-time performance metrics for a specific Atlas database deployment in a project.
View Atlas Search Metrics

    View Atlas Search metrics for Atlas clusters with at least one active Atlas Search index.

## Important Metrics

You can monitor the following metrics to quickly gauge the health of your
database deployment.

Chart

|

Description  
  
|  
  
Connections

|

Number that indicates the total active connections to the database deployment.

Monitor connections to determine whether the current connection limits are
sufficient. If necessary, upgrade the cluster tier.

To learn more, see Fix Connection Issues and Fix Lost Primary.  
  
Disk IOPS

|

Number that indicates the input operations per second.

Monitor whether disk IOPS approaches the maximum provisioned IOPS. Determine
whether the cluster can handle future workloads.

To learn more, see Fix IOPS Issues and Fix Lost Primary.  
  
Disk Usage

|

Number that indicates the total bytes of used disk space for the cluster.

Monitor the combined size of your data and MongoDB operational data (buffer,
journal, and log files) on the cluster.

To learn more, see Fix Storage Issues.  
  
Query Targeting

|

Number that indicates the efficiency of read operations run on MongoDB.

Monitor query targeting metrics to identify inefficent queries.

## Note

The changestream cursors that the Atlas Search process (`mongot`) uses for
replication can contribute to the query targeting ratio and trigger query
targeting alerts if the ratio is high.

To learn more, see Fix Query Issues.  
  
Normalized System CPU

|

Number that indicates CPU usage of all processes on the node, scaled to a
range of 0-100% by dividing by the number of CPU cores.

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.

To learn more, see Fix IOPS Issues, Fix Lost Primary, and Fix CPU Usage
Issues.  
  
Oplog GB/Hour

|

Number that indicates the average rate in gigabytes of oplog data that the
primary generates per hour.

Monitor oplog data to determine whether you have to increase the oplog size.

To learn more, see Fix Oplog Issues.  
  
Util %

|

Percentage of time that requests are issued to and serviced by disk. This
metric includes requests from any process, not just MongoDB processes.

Monitor whether utilization is high. Determine whether to increase the
provisioned IOPS or upgrade the cluster.

To learn more, see Fix IOPS Issues.  
  
## Monitoring Data Storage Granularity

Atlas stores metrics data at increasing granularity levels. For each
increasing granularity level, Atlas computes the metrics data based on the
averages from the previous granularity level. The length of retention depends
on the granularity. Atlas computes the metrics data based on the averages from
the previous granularity level.

Atlas gathers metrics data at a 1-minute granularity unless you qualify for
premium monitoring.

## Example

After 48 hours' worth of data is collected, each group of 60 minutes is
compacted into a single unit of an hour. After 63 days, each group of 24 hours
is compacted into a single unit of a day.

### Premium Monitoring Granularity

If you have at least one cluster that's `M40` or larger, Atlas automatically
enables premium monitoring for all clusters in the project. With premium
monitoring enabled, Atlas gathers metrics data at a 10-second granularity.
Premium monitoring remains enabled for all clusters in the project until you
downgrade or terminate your last `M40` cluster.

### Metrics Data Retention

Atlas retains metrics data for a period of time that depends on the
granularity of the data:

Data Period

|

Duration of Retention  
  
|  
  
10 seconds __

|

8 hours __  
  
1 minute

|

48 hours  
  
5 minutes

|

48 hours  
  
1 hour

|

63 days  
  
1 day

|

Forever  
  
 __ Premium monitoring only.

Atlas retains all database-specific statistics. MongoDB log data is retained
at a maximum rate of 2000 lines per 2 minutes.

## Free Cluster and Shared Cluster Monitoring Considerations

  * `M0` free clusters and `M2/M5` shared clusters support a subset of the metrics and charts available. For complete documentation on the limitations of `M0/M2/M5` clusters, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * Atlas pauses monitoring for `M0` free clusters which have had no connection activity for 7 days. Monitoring resumes once a successful connection occurs through the Atlas Administration API, Driver, `mongosh`, or Data Explorer.

## Serverless Instance Monitoring Considerations

  * Serverless instances support a subset of the metrics and charts available. For complete documentation on the limitations of serverless instances, see Serverless Instance Limitations.

← Fix CPU Usage IssuesReview Project Overview →

