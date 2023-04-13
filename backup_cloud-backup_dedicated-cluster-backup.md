Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Dedicated Cluster Backups

Share Feedback

On this page

  * Single-Region Cluster Backups
  * Multi-Region Cluster Backups
  * Global Cluster Backups
  * Continuous Cloud Backups
  * Consistency and Snapshots

## Single-Region Cluster Backups

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

## Multi-Region Cluster Backups

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

## Global Cluster Backups

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

## Continuous Cloud Backups

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

## Consistency and Snapshots

For clusters running MongoDB version 4.2 or and later:

  * Atlas maintains causal consistency when taking snapshots except for size statistics reported by collStats and `db.[collection].count()`. Size statistics reported by collStats and `db.[collection].count()` may be inccurate.

  * Atlas coordinates the time across all shards for sharded clusters. This ensures that snapshots include all documents written to every shard and node as of the scheduled snapshot time.

For clusters running MongoDB version 4.0 and earlier:

  * Atlas maintains crash-consistent snapshots.

  * Atlas takes snapshots from each of the shards for sharded clusters and the Config Server Replica Sets at approximately the same time.

← Back Up Your Database DeploymentShared Cluster Backups →

