Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Additional Settings

Share Feedback

On this page

  * Select the MongoDB Version of the Cluster
  * Choosing a Release Cadence
  * Configure Backup Options for the Cluster
  * M2/M5 Tier Backup Options
  * M10+ Tier Backup Options
  * Termination Protection
  * Deploy a Sharded Cluster
  * Configure the Number of Shards
  * Consideration for Upgrading a Replica Set to a Sharded Cluster
  * Enable BI Connector for Atlas
  * Read Preferences
  * Sampling Settings
  * Manage Your Own Encryption Keys
  * Prerequisites
  * Procedure
  * Configure Additional Options
  * Considerations
  * View and Edit Additional Settings
  * Set Minimum Oplog Window
  * Set Oplog Size
  * Enforce Index Key Limit
  * Allow Server-Side JavaScript
  * Set Minimum TLS Protocol Version
  * Require Indexes for All Queries
  * Default Read Concern
  * Default Write Concern
  * Set Transaction Lifetime

You can configure the following additional settings for your Atlas cluster.

## Select the MongoDB Version of the Cluster

Atlas supports creating clusters with the following tiers and MongoDB
versions:

MongoDB Version

|

Supported on `M10+`

|

Supported on Free and Shared Tiers (`M0`, `M2`, `M5`)  
  
||  
  
MongoDB 4.2

|

 __

|  
  
MongoDB 4.4

|

 __

|  
  
MongoDB 5.0

|

 __

|

 __  
  
MongoDB 6.0

|

 __

|  
  
Latest Release (auto-upgrades)

|

 __

|  
  
## Important

If your cluster runs a release candidate of MongoDB 6.0, Atlas will upgrade
the cluster to the stable release version when it is generally available.

To use a rapid release MongoDB version, you must select Latest Release for
auto-upgrades. You can't select a specific rapid release version.

As new patch releases become available, Atlas upgrades to these releases via a
rolling process to maintain cluster availability. During the upgrade to the
next rapid release version, the cluster card in the Atlas UI Database
Deployments page might show the `FCV` of your cluster instead of the MongoDB
version to reflect the features that are currently available on your cluster.

To learn more about how Atlas handles end of life of major MongoDB versions,
see What happens to Atlas clusters using a MongoDB version nearing end of
life?

## Important

Before you upgrade your cluster, refer to the current recommended best
practices for major version upgrades.

To select the MongoDB version for your cluster, use the dropdown in the
Additional Settings section of the cluster form.

You can upgrade an existing Atlas cluster to a newer major MongoDB version, if
available, when you scale a cluster. However, you can't downgrade a cluster
from one major version to a previous major version.

## Important

If your project contains a custom role that uses actions introduced in a
specific MongoDB version, you can't create a cluster with a MongoDB version
less than that version unless you delete the custom role.

### Choosing a Release Cadence

You can set your Atlas clusters to follow either a major release cadence or a
rapid release cadence.

Free-tier and shared-tier clusters must follow a major release cadence. You
can configure a dedicated-tier cluster to follow a major release cadence by
selecting a specific MongoDB version from the dropdown in the Additional
Settings section of the cluster form.

Atlas does not automatically upgrade clusters on the major release cadence.
You must schedule a manual upgrade to each new major release as it enters
general availability.

You can configure a dedicated-tier cluster to follow a rapid release cadence
by selecting Latest Release from the dropdown in the Additional Settings
section of the cluster form.

You can configure a cluster for rapid releases only if it is running the most
recent major release of MongoDB. If your cluster is running a prior major
release, manually upgrade to the most recent major release to enable the
transition to rapid release.

Atlas uses the most recent MongoDB release for clusters that follow the rapid
release cadence. Atlas automatically upgrades these clusters to the new major
_and_ rapid release versions via a rolling process to maintain cluster
availability as each release becomes available. During the upgrade to the next
rapid release version, the cluster in the Atlas UI Database Deployments page
might show the `FCV` of your cluster instead of the MongoDB version to reflect
the features that are currently available on your cluster.

## Note

If you switch a cluster from the major release to the rapid release cadence,
it will upgrade directly to the currently available rapid release. For
example, if MongoDB 6.2 is the latest rapid release and you configure a
cluster running 6.0 for rapid release, it will upgrade directly to MongoDB 6.2

You can revert a cluster that follows the rapid release cadence to the major
release cadence by selecting the most recent major release from the Select a
Version dropdown menu. However, you can only do this before the first rapid
release of the year is available. After a cluster updates from a major release
version to a rapid release version, you can't revert the cluster until the
next major release.

To learn more about MongoDB versions, see MongoDB Versioning in the MongoDB
Manual. For additional details about the rapid release cadence, see
Understanding the MongoDB Stable API and Rapid Release Cadence.

## Configure Backup Options for the Cluster

This section describes the backup configuration options for your Atlas
cluster.

### M2/M5 Tier Backup Options

Atlas automatically enables backups for `M2` and `M5` shared clusters and you
can't disable them. To learn more, see Shared Cluster Backups.

### M10+ Tier Backup Options

To enable backups for an `M10+` Atlas cluster, toggle Turn on Backup (M10 and
up) to `Yes`. If enabled, Atlas takes snapshots of your databases at regular
intervals and retains them according to your project's retention policy.

## Note

If you have a Backup Compliance Policy enabled, you can't disable Cloud
Backup. You can't disable Continuous Cloud Backup if the Backup Compliance
Policy has the Require Point in Time Restore to all clusters option set to On
without MongoDB Support. To disable Continuous Cloud Backup, the security or
legal representative specified for the Backup Compliance Policy must request
support and complete an extensive verification process.

Atlas provides the following backup options for `M10+` clusters:

Backup Option

|

Description  
  
|  
  
Legacy Backups (Deprecated)

|

## Important

### Legacy Backup Deprecated

Effective 23 March 2020, all new clusters can _only_ use Cloud Backups.

When you upgrade to 4.2, your backup system upgrades to cloud backup if it is
currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

Atlas takes incremental snapshots of the data in your cluster and lets you
restore the data from stored snapshots or from a selected point in time within
the last 24 hours. You can also query a legacy backup snapshot.

Each project has _one_ backup data center location dictated by the _first_
backup-enabled cluster created in that project. To learn more, see Snapshot
Storage Location.  
  
Continuous Cloud Backup

|

Atlas takes incremental snapshots of the data in your cluster and lets you
restore the data from those snapshots. Atlas stores snapshots in the same
cloud provider region as the replica set member targeted for snapshots.  
  
## Termination Protection

To enable Termination Protection for a cluster, toggle Termination Protection
to Yes.

If enabled, Atlas prevents users from deleting the cluster. To delete a
cluster that has termination protection enabled, you must first disable
termination protection. By default, Atlas disables termination protection for
all database deployments.

To learn more about terminating your cluster, see Terminate One Cluster.

## Deploy a Sharded Cluster

## Tip

You can configure Online Archive to move infrequently accessed data from your
Atlas cluster to a MongoDB-managed read-only federated database instance
instead of sharding your collection or upgrading your cluster tier. To learn
more about Online Archive, see Manage Online Archives.

To deploy your cluster as a sharded cluster, toggle Shard your cluster (M30
and up) to `Yes`.

Sharded clusters support horizontal scaling and consist of shards, config
servers and mongos routers:

  * Atlas deploys each shard as a three-node replica set, where each node deploys using the configured Cloud Provider & Region, Cluster Tier, and Additional Settings. Atlas deploys one `mongod` per shard node.

For cross-region clusters, the number of nodes per shard is equal to the total
number of electable and read-only nodes across all configured regions. Atlas
distributes the shard nodes across the selected regions.

  * Atlas deploys the config servers as a three-node replica set. The config servers run on M30 cluster tiers.

For cross-region clusters, Atlas distributes the config server replica set
nodes to ensure optimal availability. For example, Atlas might deploy the
config servers across three distinct availability zones and three distinct
regions if supported by the selected cloud service provider and region
configuration.

  * Atlas deploys one `mongos` router for each node in each shard. For cross-region clusters, this allows clients using a MongoDB driver to connect to the geographically "nearest" `mongos`.

To calculate the number of `mongos` routers in a cluster, multiply the number
of shards by the number of replica set nodes per shard.

You cannot convert a sharded cluster deployment to a replica set deployment.

To learn more about how the number of server instances affect cost, see Number
of Nodes.

To learn more about sharded clusters, see Sharding in the MongoDB manual.

### Configure the Number of Shards

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

### Consideration for Upgrading a Replica Set to a Sharded Cluster

If your cluster tier is `M30` or higher, you can upgrade your replica set
deployment to a sharded cluster deployment.

Once the upgrade completes, you must **restart all application clients** and
reconnect to your sharded cluster. If you don't restart the application
clients, your data might be inconsistent once Atlas begins distributing data
across shards.

  * If you are using a DNS Seed List connection string, your application automatically connects to the `mongos` for your sharded cluster.

  * If you are using a standard connection string, you must update your connection string to reflect your new cluster topology.

## Enable BI Connector for Atlas

To enable BI Connector for Atlas for this cluster, toggle Enable Business
Intelligence Connector (M10 and up) to Yes.

## Note

The MongoDB Connector for Business Intelligence for Atlas (BI Connector) is
only available for `M10` and larger clusters.

The BI Connector is a powerful tool which provides users SQL-based access to
their MongoDB databases. As a result, the BI Connector performs operations
which may be CPU and memory intensive. Given the limited hardware resources on
`M10` and `M20` cluster tiers, you may experience performance degradation of
the cluster when enabling the BI Connector. If this occurs, upgrade to an
`M30` or larger cluster or disable the BI Connector.

If enabled, select the node type from which BI Connector for Atlas should
read.

### Read Preferences

The following table describes the available read preferences for BI Connector
and their corresponding readPreference and readPreferenceTag connection string
options.

BI Connector Read Preference

|

Description

|

readPreference

|

readPreferenceTags  
  
|||  
  
Primary

|

Read from the primary node.

|

`primary`

|

None  
  
Secondary

|

Read from secondary nodes.

|

`secondary`

|

`{ nodeType : ELECTABLE }` or `{ nodeType : READ_ONLY }`  
  
Analytics

|

Read from analytics nodes.

|

`secondary`

|

`{ nodeType : ANALYTICS }`  
  
#### Node Types

The `nodeType` read preference tag dictates the type of node BI Connector for
Atlas connects to. You can specify the following values for this option:

  * `ELECTABLE` restricts BI Connector to the primary and electable secondary nodes.

  * `READ_ONLY` restricts BI Connector to connecting to non-electable secondary nodes.

  * `ANALYTICS` restricts BI Connector to connecting to analytics nodes.

## Tip

When you use the Analytics read preference, Atlas places BI Connector for
Atlas on the same hardware as the analytics nodes that BI Connector for Atlas
reads from.

By isolating electable data-bearing nodes from the BI Connector for Atlas,
electable nodes don't compete for resources with BI Connector for Atlas, thus
improving cluster reliability and performance.

For high traffic production environments, connecting to the Secondary Node(s)
or Analytics Node(s) may be preferable to connecting to the Primary Node.

For clusters with one or more analytics nodes, select Analytics Node to
isolate BI Connector for Atlas queries from your operational workload and read
from dedicated, read-only analytics nodes. With this option, electable nodes
don't compete for resources with BI Connector for Atlas, thus improving
cluster reliability and performance.

### Sampling Settings

The BI Connector generates a relational schema by sampling data from MongoDB.
You can configure the following sampling settings:

BI Connector Option

|

Type

|

Description  
  
||  
  
Schema Sample Size

|

integer

|

 _Optional._ The number of documents that the BI Connector samples for each
database when it gathers schema information. To learn more, see the BI
Connector documentation.  
  
Sample Refresh Interval

|

integer

|

 _Optional._ The frequency, in seconds, at which the BI Connector re-samples
data to recreate the schema.To learn more, see the BI Connector documentation.  
  
## Manage Your Own Encryption Keys

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

Atlas encrypts all cluster storage and snapshot volumes, ensuring the security
of all cluster data at rest (Encryption at Rest). Atlas `Project Owners` can
configure an added layer of encryption on their data at rest using the MongoDB
Encrypted Storage Engine and their Atlas-compatible Encryption at Rest
provider.

Atlas supports the following Encryption at Rest providers:

  * AWS Key Management Services

  * Azure Key Vault

  * Google Cloud KMS

### Prerequisites

  * You must configure the Atlas project for Encryption at Rest using your Key Management before you enable the feature for your Atlas clusters. To learn more, see Encryption at Rest using Customer Key Management.

  * To switch from one Encryption at Rest provider on your cluster to another, you must first disable Encryption at Rest for your cluster, then re-enable it with your desired Encryption at Rest provider. To learn more, see Encryption at Rest using Customer Key Management.

### Procedure

To start managing your own encryption keys for this cluster, toggle Encryption
using your Key Management (M10 and up) to Yes.

Atlas Encryption at Rest using your Key Management is available for `M10+`
replica set clusters. Atlas Encryption at Rest supports encrypting Back Up
Your Database Deployment **only**. You can't enable Encryption at Rest on a
cluster using Legacy Backups (Deprecated).

Managing your own encryption keys incurs an increase to the hourly run costs
of your clusters. To learn more about Atlas billing for advanced security
features, see Advanced Security.

## Important

If Atlas can't access the Atlas project key management provider or the
encryption key used to encrypt a cluster, that cluster becomes inaccessible
and unrecoverable. Exercise extreme caution before you modify, delete, or
disable an encryption key or the key management provider credentials that
Atlas uses.

## Configure Additional Options

You can configure the following `mongod` runtime options on `M10+` paid tier
clusters.

### Considerations

Atlas dynamically modifies the Oplog Size for replica sets and sharded
clusters. However, for the Minimum TLS Protocol Version and Allow Server-Side
JavaScript settings, it performs a rolling restart of the shard members and
the config server replica set. To learn more about how Atlas supports high
availability during maintenance operations, see How does MongoDB Atlas deliver
high availability?.

### View and Edit Additional Settings

To view and edit these settings:

Atlas CLI

Atlas UI

To update the advanced configuration settings for one cluster using the Atlas
CLI, run the following command:

    
    
    atlas clusters advancedSettings update <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters advancedSettings update.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Set Minimum Oplog Window

 _New in MongoDB 4.4_

Modify the retention duration for oplog entries in the oplog of the cluster.
By default, Atlas retains entries for 24 hours before they are allowed to be
removed from the oplog.

This option corresponds to modifying the `storage.oplogMinRetentionHours`
configuration file option for each `mongod` in the cluster.

### Set Oplog Size

## Note

You can see the Set Oplog Size configuration setting only if you previously
configured it for your cluster. For all new clusters, set the Minimum Oplog
Window instead.

Modify the oplog size of the cluster.

For sharded cluster deployments, this option modifies the oplog size of each
shard in the cluster.

This option corresponds to modifying the `replication.oplogSizeMB`
configuration file option for each `mongod` in the cluster.

Specify your desired Oplog Size in megabytes in the input box.

## Warning

Reducing the size of the oplog requires removing data from the oplog. Atlas
can't access or restore any oplog entries removed as a result of oplog
reduction. Consider the ramifications of this data loss before you reduce the
oplog.

## Important

  * You can't set the oplog to less than 990 megabytes.

  * Atlas places no upper limit in megabytes on the oplog. However, Atlas returns an error if the oplog size you choose leaves your cluster's disk with less than 25 percent of its capacity free.

To check the oplog size:

  1. Connect to your cluster via `mongosh`.

  2. Authenticate as a user with the `Atlas admin` role.

  3. Run the `rs.printReplicationInfo()` method.

Atlas displays the current oplog size and time.

#### Disk Space Considerations

 _Don't_ reduce the size of the oplog to increase the available disk space.
Only the oplog collection (`local.oplog.rs`) can reclaim the space that
reducing the oplog size saves. Other collections don't benefit from reducing
oplog storage.

#### Set a Fixed Oplog Size

You might want to set a fixed oplog size. For example, during migration or
during an intensive data load, you might not want the oplog to grow unbounded.

To set a fixed oplog size:

  1. Disable storage autoscaling.

  2. Set the Minimum Oplog Window to `0`.

  3. Specify your desired Oplog Size in megabytes in the input box.

### Enforce Index Key Limit

Enable or disable enforcement of the 1024-byte index key limit. Documents can
only be updated or inserted if, for all indexed fields on the target
collection, the corresponding index entries don't exceed 1024 bytes.

If disabled, `mongod` writes documents that breach the limit but _doesn't_
index them. This option corresponds to modifying the `failIndexKeyTooLong`
parameter via the `setParameter` command for each `mongod` in the cluster.

## Important

### Index Key Limit

`failIndexKeyTooLong` was deprecated in MongoDB version 4.2 and is removed in
MongoDB 4.4 and later. For MongoDB prior to 4.2, set this parameter to
`false`.

### Allow Server-Side JavaScript

Enable or disable execution of operations that perform server-side execution
of JavaScript.

  * If your cluster runs a MongoDB version less than 4.4, this option corresponds to modifying the `security.javascriptEnabled` configuration file option for each `mongod` in the cluster.

  * If your cluster runs MongoDB version 4.4 or greater, this option corresponds to modifying the `security.javascriptEnabled` configuration file option for each `mongod` and `mongos` in the cluster.

## Note

In MongoDB version 4.4 and later, `security.javascriptEnabled` applies to
mongos' as well.

### Set Minimum TLS Protocol Version

Set the minimum TLS version that the cluster accepts for incoming connections.
This option corresponds to configuring the `net.ssl.disabledProtocols`
configuration file option for each `mongod` in the cluster.

## Note

### TLS 1.0 Deprecation

If you are considering this option as a method for enabling the deprecated
Transport Layer Security (TLS) 1.0 protocol version, read What versions of TLS
does Atlas support? before proceeding. Atlas deprecation of TLS 1.0 improves
your security of data-in-transit and aligns with industry best practices.
Enabling TLS 1.0 for any Atlas cluster carries security risks. Consider
enabling TLS 1.0 only for as long as required to update your application stack
to support TLS 1.1 or later.

### Require Indexes for All Queries

Enable or disable the execution of queries that require a collection scan to
return results. This option corresponds to modifying the `notablescan`
parameter via the `setParameter` command for each `mongod` in the cluster.

### Default Read Concern

Set the default level of acknowledgment requested from MongoDB for read
operations for this cluster.

## Note

You can set the default read concern only for Atlas clusters that run MongoDB
4.4 or higher.

MongoDB 4.4 clusters default to available.

Starting with MongoDB 5.0, the default read concern for clusters is local.

### Default Write Concern

Set the default level of acknowledgment requested from MongoDB for write
operations for this cluster.

## Note

You can set the default write concern only for Atlas clusters that run MongoDB
4.4 or higher.

MongoDB 4.4 clusters default to 1.

Starting with MongoDB 5.0, the default write concern for clusters is majority.

### Set Transaction Lifetime

Set the maximum lifetime of multi-document transactions. This option
corresponds to modifying the `transactionLifetimeLimitSeconds` parameter via
the `setParameter` command for each `mongod` in the cluster.

## Important

You can't set the transaction lifetime to less than one second.

Starting with MongoDB 4.0, the transaction lifetime for clusters default to 60
seconds.

← Configure Auto-ScalingModify a Cluster →

