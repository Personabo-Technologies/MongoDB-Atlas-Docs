Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Fix Lost Primary

Share Feedback

On this page

  * Alert Conditions
  * Common Triggers
  * Fix the Immediate Problem
  * Implement a Long-Term Solution
  * Monitor Your Progress

At time `T`, no primary was detected in replica set `ABC`.

## Alert Conditions

You can configure alert conditions in the project-level alert settings page to
trigger alerts.

For more information on the alert condition, see `Replica set has no primary`.

## Common Triggers

  * The workload exceeds the cluster's throughput limits and compute resources.

  * A network issue with the cloud provider is preventing voting members of the replica set from communicating with each other, such that a primary cannot be elected.

## Fix the Immediate Problem

  * Check the cluster's metrics to determine if there are sufficient compute resources for your workload.

    * If the cluster is exhausting CPU, disk IOPS, connections, or other resources, upgrade to a cluster that supports your workload.

    * If the cluster's metrics are normal, there could be a network issue with the cloud provider. Atlas automatically attempts to repair these issues. If the problem persists, contact MongoDB Support.

## Implement a Long-Term Solution

If Atlas collects data during an election, this alert might send a false
positive. To prevent such false positives, set the alert configuration's after
waiting interval (in the configuration's Send to section).

## Monitor Your Progress

View the following charts to monitor whether the cluster is exhausting
resources:

  * Normalized System CPU

Monitor CPU usage to determine whether data is retrieved from disk instead of
memory.

If you are unable to see the usage that triggered the alert, zoom in on the
Normalized System CPU chart by clicking and dragging your mouse over the
period of interest. With a higher-resolution view you may be able to identify
acute spikes in CPU usage that weren't visible in the overview.

  * Disk IOPs

Monitor whether disk IOPS approaches the maximum provisioned IOPS. Determine
whether the cluster can handle future workloads.

  * Connections

Monitor connections to determine whether the current connection limits are
sufficient. If necessary, upgrade the cluster tier.

To learn more, see View Cluster Metrics.

← Fix Query IssuesFix Oplog Issues →

