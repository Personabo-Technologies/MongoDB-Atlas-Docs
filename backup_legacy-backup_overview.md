Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Legacy Backups (Deprecated)

Share Feedback

On this page

  * Enable Backup
  * Snapshot Storage Location
  * Snapshot Schedule

## Important

### Legacy Backup Deprecated

Effective 23 March 2020, all new clusters can _only_ use Cloud Backups.

When you upgrade to 4.2, your backup system upgrades to cloud backup if it is
currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

Atlas legacy backup takes incremental backups of data in your cluster. Use
Atlas legacy backups to restore from stored snapshots or from a selected point
in time within the last 24 hours. You can also query a legacy backup snapshot.

For sharded clusters running `FCV` 4.2 or earlier, the backup service
temporarily stops the balancer via the `mongos` to insert a marker token into
all shards and config servers in the cluster. Atlas takes a snapshot when the
marker tokens appear in the backup data. Sharded clusters running FCV 4.2 or
later don't need to stop the balancer.

## Note

You must have the `Project Owner` role for an Atlas project to manage backup
for the clusters in that project.

## Important

### Collection Limit for Atlas Legacy Backup.

Your Atlas cluster can backup or restore clusters with fewer than 100,000
files across all databases. Files include collections and indexes.

If you have one or more deployments that meet or exceed the 100,000 file
limit, contact MongoDB Support:

  1. Click Support in the left-hand navigation bar of the Atlas UI.

  2. Complete the requested fields to open a support ticket.

Back Up Your Database Deployment do not have a collection limit.

## Enable Backup

You can enable legacy backups when you:

  * create a cluster or

  * modify an existing cluster.

## Tip

### See also:

To learn how to download a Cloud Backup, see the Restore from a Locally-
Downloaded Snapshot page.

From the cluster configuration modal, toggle `Do you want to enable backup?`
to `Yes`.

### Enable Continuous Cloud Backup Restore for Sharded Clusters

## Important

This section applies only to sharded clusters running MongoDB with FCV of 4.2
or earlier. If your sharded clusters run FCV 4.2 or later, skip this section.

Sharded clusters running MongoDB with FCV of 4.2 or earlier require enabling
cluster checkpoints to support Continuous Cloud Backup restoration from a
legacy backup snapshot. Without cluster checkpoints, Atlas can only restore
from a snapshot and not from a Continuous Cloud Backup between snapshots.
After enabling legacy backups on the cluster, do the following to enable
cluster checkpoints:

1

#### Navigate to the Legacy Backup page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Project menu in the navigation bar.

  3. Click Legacy Backup in the sidebar.

2

#### Set your Snapshot Interval.

  1. Click __next to your cluster's name.

  2. Click Edit Snapshot Schedule.

  3. Click the Create cluster checkpoint every: checkbox.

  4. Select an interval from the dropdown menu.

  5. Click Submit to save your changes.

## Note

The sharded cluster balancer must pause whenever a cluster checkpoint is
created.

## Snapshot Storage Location

Each project has _one_ backup data center location dictated by the _first_
backup-enabled cluster created in that project.

For single-region Atlas clusters created after June 21st, 2017, Atlas stores
backup data for an Atlas cluster in a data center specific to the cluster's
geographic region.

For multi-region Atlas clusters, Atlas stores backup data for the cluster in a
data center specific to the geographical location of the cluster's Preferred
Region.

## Important

All additional backup-enabled clusters created in the project use the backup
data center selected during deployment of the project's _first_ backup-enabled
cluster regardless of the geographical location of the cluster region or
regions.

To change the data center location of a cluster, you must disable backups for
_all_ clusters in the project. You can then enable backups for a cluster whose
geographic region corresponds to the data center location of your choice.

Cluster Location

|

Backup Service Location  
  
|  
  
USA

|

USA  
  
Germany

|

Germany  
  
United Kingdom

|

United Kingdom  
  
Australia

|

Australia  
  
All other cluster locations

|

Ireland  
  
Atlas retains these snapshots based on the retention policy.

## Snapshot Schedule

Atlas has the following snapshot schedule, which determines the frequency and
the retention of the snapshots:

## Note

If you disable backup for a cluster or terminate a cluster, Atlas immediately
deletes the backup snapshots for the cluster.

Snapshot Schedule

|

Default Retention Policy

|

Maximum Retention Setting  
  
||  
  
Base snapshot every <x> hours

|

2 days

|

5 days

(30 days if snapshot taken every 24 hours)  
  
Daily snapshot

|

7 days

|

360 days  
  
Weekly snapshot

|

4 weeks

|

52 weeks  
  
Monthly snapshot

|

13 months

|

84 months  
  
By default, Atlas takes base snapshots every 6 hours.

To change a deployment's snapshot schedule, including the retention policy, go
to Backup. For the cluster whose snapshot schedule you wish to modify, click
the ellipsis and select Edit Snapshot Schedule menu option.

## Tip

### See also:

To modify the schedule using the API, see cloud backup schedules.

← Download Query LogsRestore a Cluster from a Legacy Backup Snapshot →

