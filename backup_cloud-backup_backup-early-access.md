Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Back Up Your Database Deployment

Share Feedback

On this page

  * Cloud Backups
  * Single-Region Cluster Backups
  * Multi-Region Cluster Backups
  * Global Cluster Backups
  * Continuous Cloud Backups
  * Consistency and Snapshots
  * Backup Scheduling, Retention, and On-Demand Backup Snapshots
  * Shared Cluster Backups
  * Limitations
  * Backup Snapshot Storage Locations
  * View `M2`/`M5` Backup Snapshots
  * Serverless Instance Backups
  * Limitations
  * View Serverless Instance Snapshots

## Cloud Backups

## Note

### Feature Unavailable in Free-Tier Clusters

This feature is not available for `M0` free clusters. To learn more about
which features are unavailable, see Atlas M0 (Free Cluster), M2, and M5
Limitations.

Atlas Cloud Backups provide localized backup storage using the native snapshot
functionality of the cluster's cloud service provider.

## Note

You must have the `Project Owner` role for an Atlas project to manage backup
for the clusters in that project.

Atlas supports cloud backup for clusters served on:

  * Microsoft Azure

  * Amazon Web Services (AWS)

  * Google Cloud Platform (GCP)

You can enable cloud backup during the cluster creation or during the
modification of an existing cluster. From the cluster configuration modal,
toggle Turn on Cloud Backup to Yes.

If you need to retain any legacy backup snapshots for archival purposes,
download them before you switch to Cloud Backup from legacy backups. To learn
how to download a snapshot, see Restore a Cluster from a Legacy Backup
Snapshot.

When you change from Legacy Backups to Cloud Backups, Atlas retains your
Legacy Backup snapshots in accordance with your legacy backup retention
policy.

## Important

### Limitations of Cloud Backup

Cloud Backups:

  * Can support sharded clusters running MongoDB version 4.0 or later.

  * Cannot restore an existing snapshot to a cluster after you add or remove a shard from it. You may restore an existing snapshot to another cluster with a matching topology.

## Note

### Sharded Cluster Balancer, FCV 4.0 databases and Cloud Backup

With databases running `FCV` 4.0 or earlier, Cloud Backup automatically
disables the balancer for snapshots if it's running. This ensures an inactive
balancer during the backup operation. When the snapshot completes, Cloud
Backup returns the balancer to its previous state.

### Single-Region Cluster Backups

With single-region cluster backups, Atlas:

  * Determines the order of nodes to try to snapshot using the following algorithm:

    1. Snapshots on a secondary. 1 Then,

    2. Snapshots the node with the lowest priority if possible. 2 Then,

    3. Snapshots incrementally from one snapshot to the next if possible. 3 Then,

    4. Snapshots node lexically first by hostname.

1 If there is a tie, Atlas skips to the next step to determine the node to
snapshot.

2 If there is a tie, Atlas then favors the node that can be snapshotted
incrementally from the previous snapshot (i.e., node using the same disk).

3 If there is a tie, Atlas then favors the node with the lexicographically
smallest hostname.

  * Once the node order is determined, tries to snapshot a node. If a selected node is unhealthy, Atlas tries to snapshot the next node that it favors.

  * Stores the snapshots in the same cloud region as the cluster.

  * Retains snapshots based on your retention policy.

Atlas automatically creates a new snapshot storage volume if the existing
snapshot storage volume becomes invalid. Atlas creates the new volume in the
same region as the cluster's current primary. Atlas then takes a full-copy
snapshot to maintain backup availability and continues using that member and
its corresponding region for further incremental snapshots.

Events that can cause an election to select a new node for the snapshot
storage volume include:

  * Changing the Atlas cluster tier,

  * Modifying the Atlas cluster's storage volume or speed,

  * Changing the Atlas cluster's region, and

  * Maintenance performed by Atlas or the cluster's cloud provider.

## Tip

### See also:

To learn more about snapshot retention, see Backup Scheduling, Retention, and
On-Demand Snapshots.

### Multi-Region Cluster Backups

With multi-region cluster backups, Atlas:

  * Determines the order of nodes to snapshot using the following algorithm:

    1. Snapshots in the highest priority region if possible. 1 Then,

    2. Snapshots on a secondary. 2 Then,

    3. Snapshots the node with the lowest priority if possible. 3 Then,

    4. Snapshots incrementally from one snapshot to the next if possible. 4 Then,

    5. Snapshots node lexically first by hostname.

1 If there is a tie, Atlas then compares based on the descending order of
priority.

2 If there is a tie, Atlas skips to the next step to determine the node to
snapshot.

3 If there is a tie, Atlas then favors the node that can be snapshotted
incrementally from the previous snapshot (i.e., node using the same disk).

4 If there is a tie, Atlas then favors the node with the lexicographically
smallest hostname.

  * Tries to snapshot a node once the node order is determined. If a selected node is unhealthy, Atlas tries to snapshot the next node that it favors.

  * Retains snapshots based on your retention policy.

Atlas automatically creates a new snapshot storage volume if the existing
snapshot storage volume becomes invalid. Atlas creates the new volume in the
same region as the cluster's current primary. Atlas then takes a full-copy
snapshot to maintain backup availability and continues using that member and
its corresponding region for further incremental snapshots.

Events that can cause an election to select a new node for the snapshot
storage volume include:

  * Changing the Atlas cluster tier,

  * Modifying the Atlas cluster's storage volume or speed,

  * Changing the Atlas cluster's highest priority region, and

  * Maintenance performed by Atlas or the cluster's cloud provider.

## Tip

### See also:

To learn more about snapshot retention, see Backup Scheduling, Retention, and
On-Demand Snapshots.

### Global Cluster Backups

Atlas can back up Global Clusters using Cloud Backups as their backup method.
Atlas restores the shards in the source cluster to the corresponding shards in
the target cluster using the same order as specified in the cluster
configuration.

## Example

`shard0` in the source cluster is restored to `shard0` in the target cluster.

## Note

If you used the API to create your Global Cluster, the zones are defined in
the `replicationSpecs` parameter in the Create a Cluster and Modify a Cluster
API endpoints.

If the cluster configurations of the source and target clusters do not match,
shard data may migrate to a different cloud provider zone than where it
resided in the source cluster. After Atlas completes the restore operation,
the MongoDB balancer for the target cluster migrates the data back to the zone
where it resided in the source cluster if your clusters meet the following
requirements:

  * Both clusters have enabled a Global Cluster on the same collection

  * Both clusters use the same shard key for the Global Writes-enabled collection

## Note

If the Global Writes-enabled collection on the target cluster does not contain
any data, the MongoDB balancer for the cluster automatically distributes any
data that you later add to the collection among the target cluster's shards.

To enable global writes on the target cluster:

  1. Click Database in the top-left corner of Atlas.

  2. Click Browse Collections beneath the target cluster on the Database Deployments page.

  3. Click Enable Global Writes.

### Continuous Cloud Backups

Continuous Cloud Backups replay the oplog to restore a cluster from a
particular point in time within a window specified in the Backup Policy.

You may opt to enable Continuous Cloud Backup restores. Configure your
continuous cloud backup window with the Backup Policy Editor.

## Note

Enabling continuous cloud backups increases the monthly cost of your cluster.

To learn more about the cost implications, see billing.

Your cluster's snapshots stay within the cloud provider's storage service
under the cluster or shard's highest priority region. Oplog backups on AWS
clusters use standard AWS S3 encryption.

## Note

All clusters with continuous cloud backups enabled store oplog data on AWS S3,
including clusters backed by Azure and Google Cloud.

The following actions cause all existing oplog backups to be deleted. All
existing snapshots remain intact, but Atlas removes previously preserved oplog
data when:

  * You disable continuous cloud backups for your cluster.

  * The cluster receives an excessive number of writes. The cluster processes a large number of writes that causes the oplog to roll over before backup collects it.

## Example

    1. You sized your oplog for one hour of its usual write traffic, say 1,000 operations.

    2. Database activity results in a large number of writes to the oplog, say 2,000 operations.

    3. The number of writes result in the oplog dropping older records. This example would lose 1,000 operations.

    4. Backup should collect operation #1, but it collects #1,001 instead.

If you change your cluster's highest priority region or if MongoDB migrates
oplog data to a different region:

  * Atlas retains data in both the old and new regions until your continuous cloud backup window is represented in the new region. Once the continuous cloud backup window is represented in the new region, Atlas deletes the data in the old region.

  * You will be billed for storage in both the old and new regions for the days following the region change. You must disable continuous cloud backup and reenable it to prevent billing in both regions.

## Note

If you disable continuous cloud backup, Atlas will delete the continuous cloud
backup history.

When you use continuous cloud backups to restore a cluster from a previous
point in time, Atlas retains the cluster's oplog. You can use continuous cloud
backups repeatedly to restore the cluster to any point in its continuous cloud
backup window **except** between when you initiated a restore and when Atlas
completes a snapshot after the restore.

### Consistency and Snapshots

For clusters running MongoDB version 4.2 or and later:

  * Atlas maintains causal consistency when taking snapshots except for size statistics reported by collStats and `db.[collection].count()`. Size statistics reported by collStats and `db.[collection].count()` may be inccurate.

  * Atlas coordinates the time across all shards for sharded clusters. This ensures that snapshots include all documents written to every shard and node as of the scheduled snapshot time.

For clusters running MongoDB version 4.0 and earlier:

  * Atlas maintains crash-consistent snapshots.

  * Atlas takes snapshots from each of the shards for sharded clusters and the Config Server Replica Sets at approximately the same time.

### Backup Scheduling, Retention, and On-Demand Backup Snapshots

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

#### Change the Backup Policy Time

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

#### Configure the Backup Policy

Each row in the Backup Policy Frequency and Retention table represents a
backup policy item. Configure the policy items and, optionally, add new policy
items to configure a new backup policy.

## Tip

Atlas displays the estimated number of snapshots associated with your changes
below the Backup Policy Frequency and Retention table.

To specify a backup policy item using the Atlas UI:

  1. Select the frequency unit from Frequency Unit for a policy item.

Alternatively, click Add Frequency Unit to add a new policy item to the backup
policy.

## Note

You cannot specify multiple Hourly and Daily backup policy items.

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

  4. (Optional) To apply the retention changes in the updated backup policy to snapshots that Atlas took previously, check Apply policy retention changes to existing snapshots.

## Note

This option affects only snapshots created by the updated policy items and
whose retention has not been updated individually with the Update Cloud Backup
Schedule API.

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
cluster. For clusters not using Encryption at Rest using Customer Key
Management you can download the latest snapshot to preserve any data stored in
the cluster.

#### Configure the Restore Window

You can replay the oplog to restore a cluster from any point in time within a
specified restore window.

To specify the restore window duration, select how long you want Atlas to
retain the oplog for point-in-time restores from the Restore Window list.

You can't configure a restore window that is longer than the Hourly Snapshot
Retention Time.

#### Configure Atlas to Automatically Copy Snapshots to Other Regions

You can configure Atlas to automatically create copies of your snapshots and
oplogs and store them in other regions. With snapshots distributed across
regions, you can still restore your cluster if the primary region goes down,
enhancing your disaster recovery capabilities to bring them in line with
internal or regulatory requirements. Additionally, you can perform direct
attach restores rather than slower streaming restores for clusters based in
the same project and region where you store copies. This reduces system
recovery time.

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

#### View Backup Snapshots

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

Snapshots taken according to the backup policy display the frequency of the
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

#### Take On-Demand Snapshots

Atlas takes on-demand snapshots immediately, unlike scheduled snapshots which
occur at regular intervals. If there is already an on-demand snapshot with a
status of `queued` or `inProgress`, you must wait until Atlas has completed
the on-demand snapshot before taking another. If there is already a scheduled
snapshot with a status of `queued` or `inProgress`, you may queue an on-demand
snapshot. You must have the `Organization Owner` or `Project Owner` role to
successfully call this endpoint.

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

## Shared Cluster Backups

Atlas takes daily snapshots of `M2` and `M5` shared clusters. Atlas takes
these snapshots automatically starting 24 hours after you create your cluster.

## Note

You must have the `Project Owner` role for an Atlas project to manage backup
for the clusters in that project.

Atlas always takes `M2` and `M5` snapshots from a secondary node to minimize
performance impact.

Atlas retains the last 8 daily snapshots, which you can download or restore to
an Atlas cluster.

### Limitations

  * Custom policies are not supported for `M2` and `M5` cluster snapshots. Atlas always takes a single daily snapshot at the same time, starting 24 hours after the cluster was created.

If you require finer-grained backups, consider upgrading to an `M10` or larger
cluster tier.

  * On-demand snapshots are not supported for `M2` and `M5` clusters.

  * You can't restore `M2` and `M5` snapshots to a sharded cluster. You can only restore `M2` and `M5` snapshots to replica sets.

  * You can't restore serverless instance snapshots to `M2` and `M5` clusters.

  * Starting with MongoDB 5.0, you can restore snapshots of clusters that run only the two most recent major versions of MongoDB to `M2` and `M5` clusters.

## Example

    * You can restore snapshots taken from clusters that run MongoDB 4.4 to an `M2` or `M5` cluster that runs MongoDB 5.0.

    * You can't restore snapshots taken from clusters that run MongoDB version earlier than 4.4 to an `M2` or `M5` cluster that runs MongoDB 5.0.

### Backup Snapshot Storage Locations

The following table indicates where Atlas stores `M2` and `M5` cluster
snapshots:

Cluster Location

|

Snapshot Storage Location  
  
|  
  
Australia

|

Australia  
  
Germany

|

Germany  
  
Hong Kong

|

Australia  
  
India, Singapore, Taiwan

|

Asia  
  
USA

|

USA  
  
All other cluster locations

|

Ireland  
  
### View `M2`/`M5` Backup Snapshots

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

Atlas displays existing snapshots in the All Daily Snapshots table. From this
table, you can restore or download your existing snapshots.

## Serverless Instance Backups

Atlas takes snapshots of serverless instances using the native snapshot
capabilities of the serverless instances's cloud service provider.

## Important

You can't disable backup of serverless instances.

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
  
To learn more, see Configure Serverless Instance Backup.

### Limitations

  * You can't download serverless instance snapshots.

  * Custom policies are not supported for serverless instance snapshots. Atlas always takes snapshots every six hours.

If you require finer-grained backups, consider migrating to a dedicated
cluster.

  * Atlas doesn't support on-demand snapshots for serverless instances.

  * You can't restore snapshots from shared clusters, dedicated clusters, or from Cloud Manager to serverless instances.

### View Serverless Instance Snapshots

Atlas displays existing snapshots on the Snapshots page.

To view your snapshots:

Atlas CLI

Atlas UI

#### View Snapshots

To return all cloud backup snapshots for the specified serverless instance in
your project using the Atlas CLI, run the following command:

    
    
    atlas serverless backups snapshots list <clusterName> [options]  
      
  
To return the details for the specified snapshot for your project using the
Atlas CLI, run the following command:

    
    
    atlas serverless backups snapshots describe [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas serverless backups snapshots list and
atlas serverless backups snapshots describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

#### View Snapshot Status

To watch the specified snapshot in your project until it reaches a completed
or failed status using the Atlas CLI, run the following command:

    
    
    atlas serverless backups snapshots watch [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas serverless backups snapshots watch.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

What is MongoDB Atlas? →

