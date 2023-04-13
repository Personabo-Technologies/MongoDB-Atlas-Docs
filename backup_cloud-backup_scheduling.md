Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Backup Scheduling, Retention, and On-Demand Snapshots

Share Feedback

On this page

  * View Backup Policies
  * Change the Backup Policy Time
  * Configure Your Backup Policy
  * Configure the Restore Window
  * Configure Atlas to Automatically Copy Snapshots to Other Regions
  * Delete a Backup Snapshot
  * View Backup Snapshots
  * Take On-Demand Snapshots

You can view and modify backup policies. You can also manage your backup
snapshots.

If you have strict data protection requirements, you can enable a Backup
Compliance Policy to protect your backup data. If you have a Backup Compliance
Policy enabled, Atlas prohibits certain actions. To learn more, see Configure
a Backup Compliance Policy.

## View Backup Policies

Atlas CLI

Atlas UI

To return the details of the backup policy for the cluster you specify using
the Atlas CLI, run the following command:

    
    
    atlas backups schedule describe <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas backups schedule describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

A backup policy has the following sections:

  * A time of day, in UTC, at which to create snapshots.

  * A frequency interval and duration of retention.

  * If PIT Restores are enabled, a PIT window that allows you to restore to any point in time in the last X days where X is the window.

## Example

The default backup policy specifies a snapshot time of `18:00` UTC and the
following four policy items:

Policy Type

|

Tier

|

Continuous Cloud Backup

|

Snapshot Taken

|

Snapshot Retained  
  
||||  
  
Hourly

|

NVMe

|

Enabled

|

Every 12 hours

|

2 days  
  
Hourly

|

non-NVMe

|

Enabled

|

Every 6 hours

|

2 days  
  
Daily

|

All

|

Either

|

Every day

|

7 days  
  
Weekly

|

All

|

Either

|

Every Saturday

|

4 weeks  
  
Monthly

|

All

|

Either

|

Last day of the month

|

12 months  
  
To learn more about Cloud Backup billing, see Cloud Backups.

## Note

If you have a Backup Compliance Policy enabled, you can't modify the backup
policy for an individual cluster below the minimum requirements set in the
Backup Compliance Policy. You can modify the cluster-level backup policy at
any time. Atlas augments any preexisting cluster-level policies to meet the
minimum requirements of the Backup Compliance Policy. All new clusters use the
Backup Compliance Policy. If you reduce the frequency of a backup schedule,
the change applies only to future backups. Any existing oplog remains for the
original window. The minimum requirements of the Backup Compliance Policy
apply.

### Change the Backup Policy Time

Atlas CLI

Atlas UI

To update the backup policy for the cluster you specify using the Atlas CLI,
run the following command:

    
    
    atlas backups schedule update [options]  
      
  
To delete the backup policy for the cluster you specify using the Atlas CLI,
run the following command:

    
    
    atlas backups schedule delete <clusterName> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas backups schedule update and atlas
backups schedule delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Configure Your Backup Policy

Each row in the Backup Policy Frequency and Retention table represents a
backup policy item. Configure the policy items and, optionally, add new policy
items to configure a new backup policy.

## Tip

Atlas displays the estimated number of snapshots associated with your changes
below the Backup Policy Frequency and Retention table.

To specify a backup policy item using the Atlas UI:

  1. Select the frequency unit from Frequency Unit for a policy item.

Alternatively, click Add Frequency Unit to add a new policy item to your
backup policy.

## Note

You can't specify multiple Hourly and Daily backup policy items.

If you have a Backup Compliance Policy enabled, only MongoDB support can
delete policy items specified in the Backup Compliance Policy. To delete
policy items specified in the Backup Compliance Policy, you must request
support and complete an extensive verification process.

  2. Select the frequency for the frequency unit from Every.

## Note

If you delete an existing backup frequency unit, the snapshots for which the
frequency was specified remain intact until they expire or you delete them.

  3. Specify the retention time for the policy item in Retention Time and the units for the retention time from the list to the right.

## Note

Atlas requires that the value specified for Retention Time for items that are
less frequent is equal to or larger than the value specified for items that
are more frequent. For example, if the hourly policy item specifies a
retention of two days or greater, the retention for the weekly snapshot must
be two weeks or greater.

You can't configure a restore window that is longer than the Hourly Snapshot
Retention Time.

If you have a Backup Compliance Policy enabled, you can't decrease the
retention time for a snapshot after it's taken.

  4. (Optional) To apply the retention changes in the updated backup policy to snapshots that Atlas took previously, check Apply policy retention changes to existing snapshots.

## Note

This option affects only snapshots created by the updated policy items and
whose retention has not been updated individually with the Modify Cloud Backup
Backup Policy API.

  5. Click Save Changes.

## Note

To take a snapshot sooner than the next scheduled snapshot, use the Take One
On-Demand Snapshot API.

## Note

If overlapping policy items generate the same snapshot, Atlas associates the
snapshot with the policy item with the longest retention time.

## Example

If the policy specifies a daily snapshot with a retention of two days and a
weekly snapshot every Saturday with a retention of three weeks, Atlas must
choose which frequency unit to associate with the snapshot taken on Saturday,
hourly or weekly.

Since the retention time for the weekly policy item is longer than that
specified for the hourly policy item, Atlas displays a frequency of Weekly in
the Frequency column on the Snapshots page for the snapshot taken on Saturday.

## Important

If you disable Cloud Backups for a cluster or terminate a cluster that had
snapshots enabled, Atlas immediately deletes the backup snapshots for that
cluster unless the Keep existing snapshots after termination option is
enabled. To learn more, see Terminate One Cluster. For clusters not using
Encryption at Rest using Customer Key Management you can download the latest
snapshot to preserve any data stored in the cluster.

### Configure the Restore Window

## Note

If you have a Backup Compliance Policy enabled, only MongoDB support can
reduce the Continuous Cloud Backup Restore Window. To reduce the Continuous
Cloud Backup Restore Window, the security or legal representative specified
for the Backup Compliance Policy must request support and complete an
extensive verification process.

You can replay the oplog to restore a cluster from any point in time within a
specified restore window.

To specify the restore window duration, select how long you want Atlas to
retain the oplog for point-in-time restores from the Restore Window list.

You can't configure a restore window that is longer than the Hourly Snapshot
Retention Time.

### Configure Atlas to Automatically Copy Snapshots to Other Regions

You can configure Atlas to automatically create copies of your snapshots and
oplogs and store them in other regions. With snapshots distributed across
regions, you can still restore your cluster if the primary region goes down,
enhancing your disaster recovery capabilities to bring them in line with
internal or regulatory requirements. Additionally, you can perform direct
attach restores rather than slower streaming restores for clusters based in
the same project and region where you store copies. This reduces system
recovery time.

If you need to restore your cluster, Atlas decides whether to use the original
snapshot or a copied snapshot for optimal restore speeds. Atlas might use
copied snapshots if you are restoring a cluster in the same region as a
snapshot copy, including multi-region clusters if the snapshots were copied to
every cluster region. Additionally, if the original snapshot becomes
unavailable due to a regional outage within your cloud provider, Atlas uses a
copy in the nearest region to enable restores regardless of the cloud region
outage.

## Note

If you have a Backup Compliance Policy enabled with the Keep all snapshots
when removing additional snapshot regions option set to On and you enable,
modify, or delete multi-region snapshots, any snapshots already taken remain.

You can use copied oplogs to perform continuous cloud backup from secondary
regions in the event the primary region of your cluster goes down.

## Note

Serverless instance backups and legacy backups don't support this
configuration.

If you enable a peering connection and restrict certain regions for Google
Cloud, you can copy snapshots to only those regions.

Snapshots taken in AWS and Azure regions are incremental. Snapshots taken for
GCP are not incremental, resulting in higher data storage and transfer costs.

To configure automatic snapshot distribution in other regions:

  1. Navigate to the Backup Policy tab. In the Additional Backup Copies section, click the arrow button to expand the pane.

  2. Toggle Copy to other regions on. You will see a table of distribution policies pre-populated with the cluster's current regions.

## Note

For a global cluster, you can enable or disable this setting independently for
each zone.

  3. In the Copy to other regions table, click Choose a region in the Region column of the row under your current region and select the region to distribute snapshots to.

## Note

You can select regions only for the same cloud provider as the primary region.
For example, if your cluster is in the AWS `us-east-1` region, you can
distribute snapshots only to other AWS regions supported by Atlas. For global
clusters, each zone may have nodes in multiple cloud providers. When you
select regions in which to store copied snapshots, you can select only regions
in the same cloud provider as the zone's primary region.

  4. In the Snapshots column, click the arrow to view the available snapshot policies for the cluster. Atlas displays options based on the backup policies for the cluster.

For example, if you set the cluster with a Daily backup policy of taking daily
5:00 PM snapshots, checking Daily in the Snapshots column enables snapshot
distribution of daily 5:00 PM snapshots. You can't set the snapshot
distribution policy to a different frequency or timing than its underlying
backup policy.

You can enable or disable any combination of the available policies on a
region-by-region basis.

## Example

The following table describes the snapshot distribution policy for a cluster
with enabled storage nodes in the AWS regions `us-east-2`, `us-west-1`, and
`us-west-2`:

Region

|

Hourly

|

Daily

|

Weekly

|

Monthly

|

On Demand

|

Point-in-Time  
  
||||||  
  
`us-east-1` (Original)

|

Every 6 hours

|

Every 2 days

|

Every Sunday

|

Last day of the month

|

Yes

|

Yes  
  
`us-east-2` (Copy)

|

Disabled

|

Disabled

|

Enabled

|

Enabled

|

Disabled

|

No  
  
`us-west-1` (Copy)

|

Enabled

|

Enabled

|

Enabled

|

Enabled

|

Enabled

|

Yes  
  
`us-west-2` (Copy)

|

Enabled

|

Enabled

|

Disabled

|

Disabled

|

Enabled

|

Yes  
  
  5. If you enabled Continuous Cloud Backup for the cluster, you can enable oplog distribution for each additional region. If you disabled Continuous Cloud Backup for the cluster, you can't enable oplog distribution for additional regions.

To delete a policy for snapshot distribution to other regions:

  1. In the Action column, click __.

  2. In the dialog box, select either Keep all snapshots in this region or Delete all snapshots in this region, and click Confirm. If you choose to keep snapshots in a disabled region, the snapshots persist until their scheduled expiration date.

Alternatively, to disable all snapshot distribution policies within a single-
region cluster or within a global cluster zone, click the Copy to other
regions toggle. As with deleting an individual policy, you can choose to keep
or delete all copied snapshots for that cluster or zone.

## Note

In the event of a cloud provider service outage in a region configured for
automatic snapshot distribution, Atlas will attempt restore using snapshots
stored in copy regions.

### Delete a Backup Snapshot

## Note

If you have a Backup Compliance Policy enabled, you can't delete a backup
snapshot.

To delete all copies of a snapshot without deleting its distribution policy,
delete the snapshot from its original region using one of the following
methods:

Atlas CLI

Atlas Administration API

Atlas UI

To delete the backup snapshot you specify using the Atlas CLI, run the
following command:

    
    
    atlas backups snapshots delete <snapshotId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas backups snapshots delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

Deleting the original snapshot by any of these methods will propagate the
deletion to all copies of that snapshot.

### View Backup Snapshots

Atlas CLI

Atlas UI

To list cloud backup snapshots for your project and cluster using the Atlas
CLI, run the following command:

    
    
    atlas backups snapshots list <clusterName> [options]  
      
  
To return the details for the snapshot you specify using the Atlas CLI, run
the following command:

    
    
    atlas backups snapshots describe <snapshotId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas backups snapshot list and atlas backups
snapshots describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

By default, Atlas displays both on-demand and policy-based snapshots. To view
only policy-based snapshots:

  1. Click Policy under View Snapshots by.

Alternatively, click On-demand to display only snapshots taken by clicking
Take Snapshot Now.

Snapshots taken according to your backup policy display the frequency of the
policy item that generated the snapshot in the Frequency column: `Monthly`,
`Weekly`, `Daily`, or `Hourly`.

## Note

If overlapping policy items generate the same snapshot, Atlas associates the
snapshot with the policy item with the longest retention time.

## Example

If the policy specifies a daily snapshot with a retention of two days and a
weekly snapshot every Saturday with a retention of three weeks, Atlas must
choose which frequency unit to associate with the snapshot taken on Saturday,
hourly or weekly.

Since the retention time for the weekly policy item is longer than that
specified for the hourly policy item, Atlas displays a frequency of Weekly in
the Frequency column on the Snapshots page for the snapshot taken on Saturday.

You can change a zone's name in the Atlas UI. If you rename a zone, old
snapshots' tooltip zone names aren't renamed.

### Take On-Demand Snapshots

Atlas takes on-demand snapshots immediately, unlike scheduled snapshots which
occur at regular intervals. If there is already an on-demand snapshot with a
status of `queued` or `inProgress`, you must wait until Atlas has completed
the on-demand snapshot before taking another. If there is already a scheduled
snapshot with a status of `queued` or `inProgress`, you may queue an on-demand
snapshot. You must have the `Organization Owner` or `Project Owner` role to
successfully call this endpoint.

## Note

If you have a Backup Compliance Policy enabled with a specified retention time
for on-demand snapshots, you can't decrease the retention time for an on-
demand snapshot after it's taken.

Atlas CLI

Atlas UI

To create a backup snapshot for your project and cluster using the Atlas CLI,
run the following command:

    
    
    atlas backups snapshots create <clusterName> [options]  
      
  
To watch for a specific backup snapshot to become available using the Atlas
CLI, run the following command:

    
    
    atlas backups snapshots watch <snapshotId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas backups snapshots create and atlas
backups snapshots watch.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Serverless Instance BackupsConfigure a Backup Compliance Policy →

