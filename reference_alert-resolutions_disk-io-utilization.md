Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Fix IOPS Issues

Share Feedback

On this page

  * Alert Conditions
  * Common Triggers
  * Fix the Immediate Problem
  * Implement a Long-Term Solution
  * Monitor Your Progress

`Disk Utilization %` alerts indicate that percentage of time during which
requests are being issued reaches a specified threshold. This threshold is
specified when the alert is created.

## Note

The utilization measurements for the following alerts include requests from
all processes, not just MongoDB processes.

## Alert Conditions

You can configure the following alert conditions in the project-level alert
settings page to trigger alerts.

`Disk utilization % on Data Partition` occurs if the percentage of time during
which requests are being issued to any partition that contains the MongoDB
collection data meets or exceeds the threshold.

`Disk utilization % on Index Partition` occurs if the percentage of time
during which requests are being issued to any partition that contains the
MongoDB index data meets or exceeds the threshold.

`Disk utilization % on Journal Partition` occurs if the percentage of time
during which requests are being issued to the partition that contains the
MongoDB journal meets or exceeds the threshold.

## Common Triggers

A few common events may lead to high Disk Utilization % and trigger these
alerts:

  * Unoptimized queries.

  * A one-time event which causes a spike in disk utilization such as an index build.

## Fix the Immediate Problem

Consider a few possible actions to help resolve `Disk Utilization %` alerts:

  * Optimize your queries.

  * Use the Atlas Performance Advisor to view slow queries and suggested indexes.

  * Review Indexing Strategies for possible further indexing improvements.

## Note

You may need to temporarily increase your cluster IOPS to create new indexes.
To change a cluster's IOPS, go to the Cluster Configuration page and:

Cloud Provider

|

Tier

|

Possible Actions  
  
||  
  
AWS

|

`M10`, `M20`

|

    * Increase Storage Capacity or

    * Upgrade Cluster Tier  
  
AWS

|

`M30` or larger

|

    * Increase Cluster IOPS or

    * Increase Storage Capacity or

    * Upgrade Cluster Tier  
  
Google Cloud

|

`M10` or larger

|

    * Increase Storage Capacity or

    * Upgrade Cluster Tier  
  
Azure

|

`M10` or larger

|

    * Increase Storage Capacity or

    * Upgrade Cluster Tier  
  
  * Analyze Query Performance to review how your queries are using your indexes.

  * Increase hardware resources, such as instance size and IOPS, in the Cluster Configuration Page.

## Implement a Long-Term Solution

### Disk IOPS Burst Credits for Atlas Clusters on Azure

Atlas clusters deployed to Azure may use credit-based bursting, but the disk
will burst only if it has burst credits accumulated in its credit bucket.
Azure also offers an on-demand bursting model, where the disk bursts whenever
its needs exceed its current capacity.

See the Azure Disk Bursting documentation for more information about how
bursting for Azure disks works.

### Conserve Burst Credits

If you regularly exceed your configured IOPS threshold, you can avoid
depleting your burst credits by increasing your configured IOPS with any of
the following actions:

  * Increase Cluster IOPS to increase the cluster's IOPS threshold.

  * Enable the Provision IOPS configuration option option. Clusters configured with this option use **Provisioned IOPS SSD** storage volumes, which do not use burst credits and offer greater IOPS thresholds. This option only applies to Atlas clusters on AWS.

  * Increase Storage Capacity. The IOPS threshold increases as you increase storage capacity. Clusters configured to use at least 1 TB of storage have baseline IOPS performance that is equal to or greater than the maximum burst performance. These volumes do not deplete burst credit balances.

  * Upgrade Cluster Tier. Larger cluster tiers include higher IOPS thresholds.

## Note

Cluster tiers `M140` and larger are deployed with at least 1 TB of storage
capacity by default. Clusters with 1 TB or more of storage capacity do not
deplete burst credit balances.

## Monitor Your Progress

These are a few possible methods to observe high Disk I/O % Utilization:

  * The Util% graph in the cluster metrics displays a high value.

  * The disk IOPS use from the Disk IOPS graph in the cluster metrics exceeds the provisioned IOPS from the Atlas cluster configuration page.

  * The Normalized System CPU metric has a high IOWait curve. IOWait measures the percentage of time the CPU is idle and waiting for an I/O operation to complete. The Normalized System CPU chart is located under the Hardware Metrics section of the Metrics tab.

← Fix Connection IssuesFix Storage Issues →

