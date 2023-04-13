Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Fix Storage Issues

Share Feedback

On this page

  * Alert Conditions
  * Common Triggers
  * Fix the Immediate Problem
  * Implement a Long-Term Solution
  * Monitor Your Progress

`Disk Space % Used` alerts indicate the percentage of used disk space on a
partition reaches a specified threshold.

## Alert Conditions

You can configure the following alert conditions in the project-level alert
settings page to trigger alerts.

`Disk space % used on Data Partition` occurs when the percentage of disk space
used on any partition that contains the MongoDB collection data meets or
exceeds a certain threshold. By default, the threshold is 90 percent of the
cluster's configured storage size.

`Disk space % used on Index Partition` occurs when the percentage of disk
space used on any partition that contains the MongoDB index data meets or
exceeds a certain threshold. You specify the threshold when you configure this
alert.

`Disk space % used on Journal Partition` occurs when the percentage of disk
space used on the partition that contains the MongoDB journal meets or exceeds
a certain threshold. You specify the threshold when you configure this alert.
This alert only occurs when journaling is enabled.

## Common Triggers

The following common events can trigger `Disk Space % Used` alerts:

  * The disk is full and Auto-Expand Storage is not enabled.

  * Auto-Expand Storage is enabled, but the disk filled too quickly for Atlas to expand the cluster's storage space. This can happen during data migration.

  * Auto-Expand Storage is enabled, but Atlas cannot expand the cluster's storage space because it has reached the maximum storage capacity for this cluster. For more information on cluster tier limits, see the Amazon Web Services, Google Cloud Platform, and Microsoft Azure instance configuration options.

## Fix the Immediate Problem

Consider the following actions to help resolve `Disk Space % Used` alerts
through the Atlas UI or API.

Atlas UI

Atlas Administration API

  * Enable Auto-Expand Storage.

## Note

If the disk fills too quickly, Atlas might not be able to expand the cluster's
storage space in time, even if Auto-Expand Storage is enabled.

  * Manually increase the Storage of this cluster in the Cluster Tier section of the configuration page.

## Implement a Long-Term Solution

Consider the following long-term solutions to help resolve `Disk Space % Used`
alerts through the Atlas UI or API.

Atlas UI

Atlas Administration API

If you have reached the maximum storage capacity for this cluster, upgrade to
a larger cluster tier in the Cluster Tier section of the configuration page.

## Monitor Your Progress

You can observe a high percentage of used disk space in the following ways:

  * In the cluster metrics, the Disk Usage graph displays the used disk space in yellow. This indicates that the used disk space is approximately 70 percent of the Atlas cluster's configured storage size.

  * Atlas nodes are unhealthy, because the used disk space reached the cluster's configured storage size.

  * The cluster refuses writes and connections from the client.

← Fix IOPS IssuesFix Query Issues →

