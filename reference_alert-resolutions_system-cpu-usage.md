Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Fix CPU Usage Issues

Share Feedback

On this page

  * Alert Conditions
  * Common Triggers
  * Fix the Immediate Problem
  * Implement a Long-Term Solution
  * Monitor Your Progress

`System CPU` alerts indicate that the CPU usage of the MongoDB process has
reached a specified threshold. This threshold is specified when the alert is
created.

## Alert Conditions

You can configure the following alert conditions in the project-level alert
settings page to trigger alerts.

`System: CPU (Steal) % is` occurs when the CPU usage exceeds the guaranteed
baseline CPU credit accumulation rate by the specified threshold. For more
information on CPU credit accumulation, refer to the AWS documentation for
Burstable Performance Instances.

## Note

The `System: CPU (Steal) % is` alert is applicable when the EC2 instance
credit balance is exhausted. Atlas triggers this alert only for AWS EC2
instances that support Burstable Performance Instances. Currently, these are
`M10` and `M20` cluster types.

`System: CPU (User) % is` occurs when the CPU usage of the MongoDB process, as
normalized by the number of CPUs, exceeds the specified threshold.

## Common Triggers

Unoptimized queries might lead to `System CPU` alerts. Also, your current
cluster tier might not support the current workload.

## Fix the Immediate Problem

Consider adding one or more indexes to improve query performance.

## Implement a Long-Term Solution

Consider upgrading your cluster to a higher tier to reduce the CPU usage
percentage utilized by the current workload. For more information on upgrading
a cluster, see Modify a Cluster.

## Monitor Your Progress

View the Normalized System CPU chart to monitor CPU usage of all processes on
the node, scaled to a range of 0-100% by dividing by the number of CPU cores.

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.

To learn more, see View Cluster Metrics.

← Fix Oplog IssuesReview Database Deployment Metrics →

