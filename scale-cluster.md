Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Modify a Cluster

Share Feedback

On this page

  * Atlas Configuration Options
  * Considerations
  * Edit a Cluster
  * Modify the Cluster Type
  * Modify the Global Cluster Configuration
  * Modify the Cloud Provider & Region
  * Modify the Cluster Tier
  * Modify Additional Settings
  * Review and Apply Your Changes
  * Convert a Replica Set to a Sharded Cluster

You can modify your cluster after initial configuration.

  * For a summary of available options, see Atlas Configuration Options.

  * For in-depth configuration steps, see Edit a Cluster and the options that follow.

For more information about the impact, cost, and backup policy of your cluster
changes, see Considerations.

## Atlas Configuration Options

You can change the following options of your Atlas cluster:

Setting

|

Action

|

Limitations  
  
||  
  
Cluster Type

|

Change the cluster type.

|

You can only move from a shared cluster to a dedicated cluster or a serverless
instance.  
  
Global Cluster Configuration

|

Enable Global Writes for your cluster or change existing global cluster
configurations.

|

After you enable Global Writes for a cluster, you can't disable them.  
  
Cloud Provider & Region

|

Select a different provider to change the cloud provider for your dedicated
clusters. If you created an Atlas cluster on GCP or Azure before October 2020
when Atlas added support for multi-cloud clusters, changing to a different
provider changes the connection string to your new cluster.

Consider scheduling a time to update your applications with the new connection
string to connect to the cluster again. Atlas migrates data to the new
cluster.

|

Adding or moving a node to a region without a primary node or without an
existing secondary node requires each newly migrated replica set member to
perform an initial sync.  
  
Deploy or Configure a multi-cloud, multi-region cluster

|

Deploy or modify a multi-cloud, multi-region cluster.

|

None  
  
Cluster Tier

|

Change the cluster tier.

|

If your cluster uses NVMe storage, Atlas must perform an initial sync.  
  
Cluster Storage Options

|

Change the storage options for the cluster tier.

When you increase the storage capacity of a cluster, Atlas increases the
cluster's oplog size. Atlas scales the oplog to 5% of the cluster capacity,
not to exceed 50 GB. NVMe storage requires an oplog which is 10% of the
storage capacity. Atlas doesn't change the oplog size if it exceeds 5% of the
new storage capacity (10% in the case of NVMe storage).

As cluster storage capacity decreases, Atlas doesn't change the oplog size
unless it exceeds a certain maximum determined according to MongoDB best
practices.

|

Clusters using NVMe storage have a fixed size for each cluster tier.  
  
Cluster Autoscaling Options

|

Change the cluster's autoscaling options.

|

None  
  
MongoDB Version

|

Upgrade the major MongoDB version of the cluster.

|

You can't downgrade the MongoDB version.  
  
Deploy a Sharded Cluster

|

Upgrade a replica set to a sharded cluster.

|

You can't reverse this upgrade.

Atlas allows Sharded Clusters for `M30` or larger clusters.

## Note

You can't convert a replica set to a sharded cluster when either of the
following Atlas App Services features is enabled for the cluster:

  * A database trigger with the Document Preimage configuration option enabled, or

  * Atlas Device Sync.

  
  
Modify the Number of Shards

|

Set the number of shards for a sharded cluster.

|

Reducing the number of shards takes some time. Atlas removes shards in
descending order based on the number in in their `"_id"` field. Any subsequent
MongoDB configuration changes start after Atlas removes the shards.

## Important

When you remove a shard, Atlas uses the movePrimary command to move any
unsharded databases in that shard to a remaining shard.

All sharded collections remain online and available during the shard removal
process. However, read or write operations to unsharded collections during the
`movePrimary` operation can result in unexpected behavior, including migration
failure or data loss.

We recommend moving the primary shard for any databases containing unsharded
collections before removing the shard.

For more information, see Remove Shards from an Existing Sharded Cluster.

Atlas allows Sharded Clusters for `M30` or larger clusters.  
  
Enable or Disable Backup

|

Enable or disable backups for the cluster.

|

Atlas enables backups for M2 and M5 clusters automatically. You can't disable
backup for clusters on those tiers.  
  
Enable or Disable the Business Intelligence Connector

|

Enable or disable the BI Connector for Atlas for this cluster.

The MongoDB Connector for Business Intelligence for Atlas (BI Connector) is
only available for `M10` and larger clusters.

The BI Connector is a powerful tool which provides users SQL-based access to
their MongoDB databases. As a result, the BI Connector performs operations
which may be CPU and memory intensive. Given the limited hardware resources on
`M10` and `M20` cluster tiers, you may experience performance degradation of
the cluster when enabling the BI Connector. If this occurs, upgrade to an
`M30` or larger cluster or disable the BI Connector.

|

None  
  
Manage your own encryption keys

|

Enable or disable using your own encryption keys with this cluster.

|

None  
  
Click Apply Changes when complete.

## Considerations

### Migration, Availability, and Performance Impact

Making changes to a cluster often requires migrating to new servers and
storage volumes. The time required for an initial sync and resynchronizing
data across storage volumes increases linearly with the amount of data in the
cluster.

The following migrations require an initial sync:

  * Upgrades from a free clusters or shared clusters (`M0`, `M2`, and `M5` clusters) to a higher cluster tier.

  * Changes from general to NVMe storage volumes and from NVMe to general storage.

  * Upgrades or downgrades from one NVMe cluster tier to another, initiated either manually or via auto-scaling. NVMe clusters auto-scale to the next higher tier when 90% of the available storage space is consumed.

  * Changes that require a replacement of an NVMe-backed Atlas cluster, such as region changes.

  * For clusters deployed to Azure, changes to the Cluster Class.

To maximize availability:

  * For a replica set, Atlas migrates one node at a time, starting with the secondary nodes first and then the primary.

  * For a sharded cluster, Atlas performs the migration of the shards independently of each other. For each shard (i.e. replica set), Atlas migrates one node at a time, starting with the secondary nodes first and then the primary.

Retryable writes should prevent any write errors during the election of a new
primary. On average, an election can take five seconds.

Migration can affect performance if your primary is already reaching
operational capacity: each newly migrated replica set node must perform an
initial sync from the primary, adding to the operational load. Migrations can
also affect performance if you set read preferences to read from secondaries:
the replica set is down one secondary during the migration.

If the workload on the Atlas cluster is such that it impedes operations,
including the ability to scale, MongoDB Atlas may, in some situations, create
indexes in your cluster as a safeguard.

### Billing

As you change your cluster, you can compare the costs of different options
before applying them. The Cluster Overview box displays the cost of the
selected configuration, excluding data transfer.

## Important

### Free Clusters

Upgrading an `M0` free cluster to an `M2` or greater paid tier cluster starts
billing for the cluster. See Manage Billing for complete documentation on
Atlas billing.

The following sections provide complete documentation for each of the Atlas
cluster scaling configuration options.

### Backup

As of MongoDB version 4.2, Legacy Backups are deprecated in favor of Cloud
Backups. When you upgrade to version 4.2 or later, your backup system upgrades
to cloud backup if it is currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

## Edit a Cluster

Atlas CLI

Atlas UI

You can modify any of the cluster settings on this page using the Atlas CLI.

To update an Atlas cluster using the Atlas CLI, run the following command:

    
    
    atlas clusters update [clusterName] [options]  
      
  
To upgrade the cluster tier, disk size, and/or MongoDB version for an `M0`,
`M2`, or `M5` Atlas cluster using the Atlas CLI, run the following command:

    
    
    atlas clusters upgrade [clusterName] [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas clusters update and atlas clusters
upgrade.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Edit Advanced Settings

To update the advanced configuration settings for one cluster using the Atlas
CLI, run the following command:

    
    
    atlas clusters advancedSettings update <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters advancedSettings update.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Modify the Cluster Type

If you have a shared cluster, you can change it to a dedicated cluster or a
serverless instance.

To convert your shared cluster to a serverless instance, see Convert a Shared
Cluster to a Serverless Instance.

To upgrade your `M0`, `M2`, or `M5` cluster to an `M10+` cluster, complete the
following steps:

1

### At the top of your configuration settings, click the Dedicated tab.

2

### Select your preferred cluster tier.

To learn more, see Modify the Cluster Tier.

Dedicated clusters have more configuration options than shared clusters.

## Note

### Considerations

  * You can't change a dedicated cluster to a shared cluster.

  * You can't change dedicated clusters to serverless instances

  * You can't change serverless instances to clusters.

For a full list of serverless instance limitations, see Serverless Instance
Limitations

## Modify the Global Cluster Configuration

## Important

You can't disable Global Writes for a cluster once deployed.

You can enable global writes for your cluster or modify existing global
cluster configurations.

## Tip

### See also:

  * Manage Global Clusters.

  * Create a Global Cluster.

## Modify the Cloud Provider & Region

## Note

### Considerations

`M0`, `M2`, or `M5` Tier Clusters

    You can modify the cloud provider when you upgrade to an `M10` or larger cluster.
`M10` or larger Tier Clusters

    You can select a different provider to change the cloud provider for your dedicated clusters.

Changing to a different provider could change the connection string to your
new cluster if your old cluster was deployed on GCP or Azure before October
2020. Consider scheduling a time to update your applications with the new
connection string to resume connectivity to the cluster. Atlas migrates data
to the new cluster.

  * To view the current cloud providers and regions for this cluster, select Cloud Provider & Region.

  * To modify the cloud providers and regions applied to this cluster, follow the procedures on Electable Nodes for High Availability.

  * To add electable nodes to your cluster during a regional outage, follow the procedure on Reconfigure a Replica Set During a Regional Outage.

  * To upgrade from an Atlas free- or shared cluster, select from the available cloud providers.

## Tip

### See also:

  * Cloud Providers and Regions.

  * Move a Cluster to a Different Region.

### View Available Regions

To list available regions that Atlas supports for new deployments using the
Atlas CLI, run the following command:

    
    
    atlas clusters availableRegions list [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters availableRegions list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Modify the Cluster Tier

You can change the cluster tier, as well as the memory, storage, and IOPS
(speed) specifications for the selected cluster.

## Note

If you have a Backup Compliance Policy enabled, you can't modify the cluster
tier to a tier that doesn't support cloud backup.

### Free Cluster and Shared Cluster Considerations

  * You can't downgrade an `M10+` dedicated cluster to an `M0` free cluster or `M2/M5` shared cluster.

  * Changing the cluster tier requires downtime in the following scenarios:

  * You change from an `M0` free cluster or `M2/M5` shared cluster to an `M10` or larger cluster tier.

  * You change from an `M0` free cluster to an `M2/M5` shared cluster.

  * You change from an `M2` shared cluster to an `M5` shared cluster.

To prevent data corruption, halt write operations to your cluster for the
duration of your upgrade.

### Procedure

Select your preferred cluster tier. The selected instance size dictates the
memory, storage, and IOPS specification for each data-bearing server [1] in
the cluster.

## Warning

Upgrading from a tenant (free or shared) tier to a dedicated cluster tier:

  * deletes the current cluster

  * deletes any backup snapshots for that cluster

To keep your existing snapshots, download those snapshots.

## Tip

### See also:

  * Snapshot Schedule

  * Select Cluster Tier

From the Cluster Tier section, you can also:

  * Customize Cluster Storage

  * Configure Autoscaling Options

For `M10+` clusters, you can select a cluster tier appropriately sized for
your analytics workload. To learn more, see Analytics Nodes for Workload
Isolation.

## Modify Additional Settings

You can set the following options:

  * Upgrade the MongoDB Version of the Cluster

  * Enable or Disable Backup for the Cluster

  * Enable or Disable Termination Protection for the Cluster

  * Scale your Replica Set to a Sharded Cluster

  * Modify the Number of Shards

  * Enable or Disable BI Connector for Atlas for the Cluster

  * Enable Encryption at Rest

  * Configure Additional Configuration Options

### Upgrade the MongoDB Version of the Cluster

## Important

Before you upgrade your cluster, refer to the current recommended best
practices for major version upgrades.

  1. Select Additional Settings to view the currently configured MongoDB version for the cluster.

Atlas always upgrades the cluster to the latest stable release of the
specified version via a rolling process to maintain cluster availability.

You cannot downgrade the cluster to an earlier MongoDB version.

You can switch from using the Latest Release to using a specific release only
if the latest MongoDB version is a major release.

  2. From the Select a version dropdown, select the new MongoDB version.

## Note

If the FCV of your cluster is set and if the FCV is below the MongoDB version
of your cluster, the cluster in the Atlas UI Database Deployments page shows
the `FCV` of your cluster to reflect the features that are currently available
on your cluster during the upgrade. After Atlas upgrades your cluster to the
new version, the cluster in the Atlas UI Database Deployments page shows the
new MongoDB version of your cluster.

Atlas supports the following upgrade paths:

    * MongoDB 4.0 -> MongoDB 4.2

    * MongoDB 4.2 -> MongoDB 4.4

    * MongoDB 4.4 -> MongoDB 5.0

    * MongoDB 5.0 -> Latest Release

## Note

If you enabled backup for your cluster and want to upgrade to MongoDB 4.2 or
later, you must enable Back Up Your Database Deployment if Legacy Backups are
currently enabled.

### Enable or Disable Backup for the Cluster

Backups are automatically enabled for `M2` and `M5` shared clusters and can't
be disabled.

## Tip

### See also:

Shared Cluster Backups.

To enable backups for an `M10+` Atlas cluster, toggle Turn on Cloud Backup
(M10 and up) to `Yes`. If enabled, Atlas takes snapshots of your databases at
regular intervals and retains them according to your project's retention
policy.

For detailed descriptions of the available backup options, see Configure
Backup Options for the Cluster.

### Enable or Disable Termination Protection for the Cluster

To enable Termination Protection for a cluster, toggle Termination Protection
to Yes.

If enabled, Atlas prevents users from deleting the cluster. To delete a
cluster that has termination protection enabled, you must first disable
termination protection. By default, Atlas disables termination protection for
all database deployments.

## Tip

### See also:

Terminate One Cluster.

### Scale your Replica Set to a Sharded Cluster

## Note

You can't convert a replica set to a sharded cluster when either of the
following Atlas App Services features is enabled for the cluster:

  * A database trigger with the Document Preimage configuration option enabled, or

  * Atlas Device Sync.

To deploy your cluster as a sharded cluster, toggle Shard your cluster (M30
and up) to `Yes`.

Once the upgrade completes, you must **restart all application clients** and
reconnect to your sharded cluster. If you don't restart the application
clients, your data might be inconsistent once Atlas begins distributing data
across shards.

  * If you are using a DNS Seed List connection string, your application automatically connects to the `mongos` for your sharded cluster.

  * If you are using a standard connection string, you must update your connection string to reflect your new cluster topology.

## Tip

### See also:

Deploy a Sharded Cluster.

### Modify the Number of Shards

This field is visible only if the deployment is a sharded cluster.

You can set the number of shards to deploy with the sharded cluster. Your
cluster can have between 1 and 50 shards, inclusive.

If you are reducing the number of shards in your sharded cluster, Atlas
removes shards in descending order based on the number in the `"_id"` field
(see Sharded Cluster Configuration). For example, consider a sharded cluster
with the following three shards:

  * `"shard0"`

  * `"shard1"`

  * `"shard2"`

If you set the number of shards to two, Atlas removes `"shard2"` from the
cluster.

## Important

When you remove a shard, Atlas uses the movePrimary command to move any
unsharded databases in that shard to a remaining shard.

All sharded collections remain online and available during the shard removal
process. However, read or write operations to unsharded collections during the
`movePrimary` operation can result in unexpected behavior, including migration
failure or data loss.

We recommend moving the primary shard for any databases containing unsharded
collections before removing the shard.

For more information, see Remove Shards from an Existing Sharded Cluster.

Don't create a sharded cluster with a single shard for production
environments. Single-shard sharded clusters don't provide the same benefits as
multi-shard configurations.

### Enable or Disable BI Connector for Atlas for the Cluster

To enable BI Connector for Atlas for this cluster, toggle Enable Business
Intelligence Connector (M10 and up) to Yes.

## Tip

### See also:

Enable BI Connector for Atlas.

### Enable Encryption at Rest

To enable Atlas Encryption at Rest for this cluster using your KMS, toggle
Manage your own encryption keys (M10 and up) to Yes. To learn more, see Manage
Your Own Encryption Keys.

## Note

All changes to customer KMS require an initial sync.

### Configure Additional Configuration Options

Configure additional options for your cluster from this section.

For details on these options, see Configure Additional Options.

## Review and Apply Your Changes

Click Review Changes to review the changes you have made.

The Review Changes page displays a complete side-by-side summary of the
modified attributes with any warnings or notes pertaining to the changes. The
original attribute settings are listed on the left and the corresponding new
settings with changes in pricing are listed on the right.

Atlas displays all warnings and notes related to the change at the top. These
include changes that:

  * Can't be rolled back

  * Require an initial sync

  * Result in expected delays in execution, increase in workload, or downtime.

Once you have reviewed the changes, click Apply Changes to apply them to your
cluster.

If you are upgrading from an `M0` free cluster, Atlas prompts you to enter
payment information before applying your changes.

[1]|  For replica sets, the data-bearing servers are the servers hosting the
replica set nodes. For sharded clusters, the data-bearing servers are the
servers hosting the shards. For sharded clusters, Atlas also deploys servers
for the config servers; these are charged at a rate separate from the cluster
costs.  
|  
  
## Convert a Replica Set to a Sharded Cluster

You can convert a replica set to a sharded cluster.

### Prerequisites

To convert your replica set to a sharded cluster:

  * Your cluster must be an `M10+` cluster.

  * You must have the `Project Cluster Manager` or higher role.

### Procedure

1

#### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

#### Click the cluster name to view cluster details.

3

#### Click Configuration in the Overview tab to view the page where you can
edit your cluster settings.

4

#### Expand Additional Settings to modify your cluster configuration.

5

#### Enable sharding in the Shard your cluster section by setting the toggle
to On.

## Note

After you convert a replica set to a sharded cluster, you can't convert it
again to a replica set.

6

#### Select the number of shards from the dropdown.

Sharding supports high throughput and large datasets, and you can increase the
number of shards as data requirements grow. By default, Atlas creates two
shards.

7

#### Click Review Changes to review the changes to billing and when satisfied,
click Apply Changes.

It may take some time for Atlas to deploy the changes. Please wait until Atlas
has converted your cluster before proceeding to the next step.

8

#### Restart all application clients and reconnect to the sharded cluster.

If you don't restart the application clients, your data might be inconsistent
after Atlas begins distributing data across shards.

  * If you are using a DNS Seed List connection string, your application automatically connects to the `mongos` for your sharded cluster.

  * If you are using a standard connection string, you must update your connection string to reflect your new cluster topology.

  * If you are using private endpoints to connect to your Atlas cluster, perform a rolling restart of your applications to connect to the `mongos` for your sharded cluster without any downtime.

To learn more, see Connect to a Database Deployment.

9

#### Distribute data across the shards in your cluster.

To shard the collection whose data you want to distribute, see
`sh.shardCollection()` for more information.

## Note

If you run `sh.shardCollection()` on an unsharded collection with Atlas Search
indexes, the Atlas Search indexes might enter an invalid state after sharding.
To mitigate this issue, you can create a new index on the collection after
sharding, or contact support to restart the `mongot` processes on the nodes.

10

#### Change any cluster-wide settings.

If you want to make further changes to the sharded cluster, see Modify a
Cluster for more information on the cluster-wide settings that you can modify.

← Configure Additional SettingsConvert a Shared Cluster to a Serverless
Instance →

