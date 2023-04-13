Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Back Up, Restore, and Archive Data

Share Feedback

Backups are copies of your data that encapsulate the state of your cluster at
a given time. Backups provide a safety measure in the event of data loss. If
you have strict data protection requirements, you can enable a Backup
Compliance Policy to protect your backup data.

## Note

You must have the `Project Owner` role for an Atlas project to manage backups
for or to restore a backup to clusters in that project.

## Considerations

Be aware that:

  * Atlas backups are not available for `M0` free clusters. You may use mongodump to back up your `M0` cluster data and mongorestore to restore that data. To learn how to manually back up your data, see Command Line Tools.

  * You must restore the backup to a cluster running either the same major release version, or the next higher one. Atlas doesn't support restoring to older versions.

You can still use backups made before an upgrade.

## Example

To restore a 4.0 cluster to 4.2:

    1. Restore the old 4.0 backup to another 4.2 cluster.

    2. Upgrade the restored cluster to 4.2.

## Cloud Backups

 _Available in M10+ Clusters._

Atlas uses the native snapshot capabilities of your cloud provider to support
full-copy snapshots and localized snapshot storage.

Atlas supports Cloud Backups on:

  * Microsoft Azure

  * Amazon Web Services (AWS)

  * Google GCP

To learn more, see Back Up Your Database Deployment.

To learn how to restore cluster from a Cloud Backup, see Restore from a
Scheduled or On-Demand Snapshot.

## M2 / M5 Snapshots

Backups are automatically enabled for `M2` and `M5` shared clusters and can't
be disabled. Atlas takes daily snapshots of your `M2` and `M5` clusters which
you can restore to clusters tiers `M2` or greater.

To learn more about `M2` / `M5` daily snapshots, see Shared Cluster Backups.

To learn how to restore cluster from `M2` / `M5` snapshots, see Restore from a
Scheduled or On-Demand Snapshot.

## Serverless Instance Snapshots

Atlas uses the native snapshot capabilities of your cloud provider to support
full-copy snapshots and localized snapshot storage.

Backups are automatically enabled for serverless instances. You can't disable
serverless instance backups.

Atlas offers the following backup options for serverless instances:

Option

|

Description  
  
|  
  
Serverless Continuous Backup

|

Atlas takes incremental snapshots of the data in your serverless instance
every six hours and lets you restore the data from a selected point in time
within the last 72 hours. Atlas also takes daily snapshots and retains these
daily snapshots for 35 days. To learn more, see Serverless Instance Costs.  
  
Basic Backup

|

Atlas takes incremental snapshots of the data in your serverless instance
every six hours and retains only the two most recent snapshots. You can use
this option for free.  
  
You can restore serverless instance snapshots to other serverless instances
and dedicated clusters.

To learn more, see:

  * Configure Serverless Instance Backup

  * Serverless Instance Backups

  * Restore from a Scheduled or On-Demand Snapshot

## Legacy Backups

 _Available in M10+ Clusters._

## Important

### Legacy Backup Deprecated

Effective 23 March 2020, all new clusters can _only_ use Cloud Backups.

When you upgrade to 4.2, your backup system upgrades to cloud backup if it is
currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

Atlas uses incremental snapshots to continuously back up your data. Continuous
backup snapshots are typically just a few seconds behind the operational
system.

Atlas ensures continuous cloud backup of replica sets and consistent, cluster-
wide snapshots of sharded clusters.

For each Atlas project with legacy backups enabled, Atlas stores the legacy
backup snapshots in the backup data center location where legacy backups were
_first_ enabled for a cluster in the project.

Continuous snapshots support restoring from the full snapshot or from a
Continuous Cloud Backup between snapshots. You can also query a continuous
snapshot.

With Atlas legacy backup, the total number of collections across all databases
in a Atlas cluster can't be equal to or exceed `100,000`.

To learn more about Legacy Backups, see Legacy Backups (Deprecated).

To learn how to restore cluster from a Legacy Backup, see Restore a Cluster
from a Legacy Backup Snapshot.

← Atlas Search ChangelogBack Up Your Database Deployment →

