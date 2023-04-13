Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Shard a Global Collection

Share Feedback

On this page

  * Shard a Global Collection for Global Writes in the Atlas UI
  * Required Roles
  * Considerations
  * Procedure
  * Global Cluster Sharding Reference
  * Sharding Collections for Global Writes
  * Error Handling
  * Sharding Collections without Global Writes
  * Unsharded Collections in Global Write Clusters

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

## Shard a Global Collection for Global Writes in the Atlas UI

## Note

  * Global writes are only supported on global clusters, which require an `M30+` cluster tier.

  * This document assumes prior knowledge of sharding semantics. Review the Sharding documentation before continuing with this tutorial.

In sharded clusters, you can create zones of sharded data based on the shard
key. Your zones can segment data based on geographic area. To learn more about
sharding based on geographic area, see Segmenting Data by Location.

The Atlas UI supports sharding Global Write collections only inside of a
global cluster. To shard non-Global-Write collections, you must use `mongosh`
or application code. To learn more, see Deploy a Sharded Cluster.

### Required Roles

You must have the `Project Owner` or `Organization Owner` role for the
cluster's Atlas project to shard a collection for Global Writes in the Atlas
UI.

### Considerations

Review the restrictions and compatibility requirements for Sharding
Collections for Global Writes before beginning this procedure.

You can configure Online Archive to move infrequently accessed data from your
Atlas cluster to a MongoDB-managed read-only federated database instance
instead of sharding your collection or upgrading your cluster tier. To learn
more about Online Archive, see Manage Online Archives.

After selecting a shard key via the Atlas UI, Atlas attempts to shard the
target collection. During this period, ensure that no user manually shards the
collection. If Atlas detects that the target collection was sharded with a
different key than the one selected via the Atlas UI, Atlas stops the
procedure and displays a warning for that collection in the Atlas UI. You can
click Unmanage Collection to clear the warning. This action removes the
collection from Atlas management while leaving the underlying collection and
the manually chosen shard key intact.

#### Update the Shard Key Value

Starting in MongoDB 4.2, you can update a document’s shard key value unless
the shard key field is the immutable `_id` field. To learn more, see Change a
Document’s Shard Key Value.

In MongoDB 4.0 and earlier, you can't update the value of a shard key field in
an existing document in a Global Writes-enabled collection.

## Important

### Shard Key Values and Global Clusters

In all MongoDB versions, you can't reshard a collection on a Global Cluster.
To learn more, see Sharding Collections for Global Writes.

### Procedure

To shard a collection in a Global Cluster:

1

#### Click Database in the left navigation pane.

2

#### Click the Browse Collections button below the cluster that contains the
collection that you want to shard.

3

#### Click the collection that you want to shard.

4

#### Click the Global Writes tab.

5

#### Enter the second field of the compound shard key in Second shard key
field.

6

#### Optional: Expand Advanced Shard Key Configuration section to specify how
to shard the collection.

You can choose one of the following:

|  
  
|  
  
Default

|

Atlas uses the document that specifies the field or fields as the shard key.  
  
Use unique index as the shard key

|

Atlas uses the underlying index to enforce a unique constraint on the shard
key of the Global Collection.  
  
Use hashed index as the shard key

|

Atlas distributes the sharded data evenly by hashing the second field of the
shard key. This option is only available for Atlas clusters running MongoDB
v4.4 or later.

You can optionally select Pre-split data for even distribution to specify
whether to perform initial chunk creation and distribution for an empty or
non-existing collection based on the defined zones and zone ranges for the
collection.

If you select the Pre-split data for even distribution option, you can also
specify the minimum number of chunks to create initially when sharding an
empty collection with a hashed shard key. Initial chunk distribution allows
Atlas to setup zoned sharding quickly. The number of chunks the Atlas creates
depends on the number of zones that you define. By default, Atlas creates one
chunk per location code and distributes chunks evenly across all shards.  
  
To learn more about these options, see Global Cluster Sharding Reference.

7

#### Click Shard Collection.

Atlas displays the compound shard key near the top of the Global Writes tab
after configuring the collection.

## Global Cluster Sharding Reference

The following sections describe sharding behavior and how to enable sharding
for Manage Global Clusters.

### Sharding Collections for Global Writes

Unsharded collections must meet the following compatibility requirements
_prior to sharding_ to use Global Writes when sharded:

  * Every document in the collection **must** include a `location` field.

  * The value of the `location` field **must** be either an ISO-3166-1 alpha 2 country code (`"US"`, `"DE"`, `"IN"`) _or_ a supported ISO-3166-2 subdivision code (`"US-DC"`, `"DE-BE"`, `"IN-DL"`). Documents that don't match this criteria can't be routed to any shard in the cluster. To view the complete list of currently supported country or subdivision codes, see https://cloud.mongodb.com/static/atlas/country_iso_codes.txt.

A shard key on the `location` field alone might result in bottlenecks,
especially for workloads where a subset of countries or subdivisions receive
the majority of write operations. Atlas Global Writes requires a compound
shard key to facilitate the efficient distribution of sharded data across the
cluster. Atlas Global Cluster shard keys share the same restrictions as
MongoDB shard keys. The following Atlas Global Cluster limitations apply:

  * The first field of the compound shard key must be `location` and _can't_ be hashed.

  * There can only be one secondary shard key field in a compound shard key.

  * Starting in MongoDB version 4.4, the secondary shard key field of a compound shard key _can_ be hashed.

  * The secondary shard key field _can't_ be an array.

## Tip

### See also:

To learn more about:

  * Choosing a secondary shard key field and the effect of shard key choices on data distribution, see Choosing a Shard Key.

  * Shard key limitations, see Shard Key Limitations.

  * Available hashed sharding options, see Hashed Sharding Options.

## Important

### Changing the Shard Key

After sharding, what you can modify depends on the version of MongoDB that you
run:

MongoDB Version

|

Modify Shard Key Keys

|

Modify Shard Key Values  
  
||  
  
MongoDB 4.0

|

No

|

No  
  
MongoDB 4.2

|

No

|

Yes  
  
MongoDB 4.4

|

Yes, add fields to a key using the Atlas UI only.

|

Yes  
  
MongoDB 5.0

|

Yes, add fields to a key using the Atlas UI only.

|

Yes  
  
In all MongoDB versions, you can't reshard a collection on a Global Cluster.

The Atlas UI supports creating sharded collections with specific validations
for Global Writes.

## Tip

### See also:

To learn more, see Shard a Global Collection for Global Writes in the Atlas
UI.

You can also use `mongosh` to execute the `sh.shardCollection()`. After
sharding the collection, you must use the Atlas UI to enable Global Writes for
that collection.

## Note

If you run `sh.shardCollection()` on an unsharded collection with Atlas Search
indexes, the Atlas Search indexes might enter an invalid state after sharding.
To mitigate this issue, you can create a new index on the collection after
sharding, or contact support to restart the `mongot` processes on the nodes.

## Tip

### See also:

To learn more about sharding collections via the Atlas UI, see Shard a Global
Collection for Global Writes in the Atlas UI.

#### Hashed Sharding Options

Shard keys use hashed sharding and pre-split data for even distribution. This
is only available on Atlas clusters running MongoDB 4.4 and later.

Atlas distributes the sharded data evenly by hashing the second field of the
shard key if you perform one of the following actions:

  * Enable the use of the hashed index shard keys by selecting Use hashed index as the shard key in the Atlas UI.

  * Set `isCustomShardKeyHashed` through the API.

You can optionally specify whether to perform initial chunk creation and
distribution for an empty or non-existing collection. This action is based on
the defined zones and zone ranges for the collection. To do this, perform one
of the following actions:

  * Select Pre-split data for even distribution in the Atlas UI.

  * Set `presplitHashedZone` using the API.

When you create a sharded collection using a compound hashed shard key for
Global Clusters, Atlas creates at least 1 chunk per location code and attempts
to distribute chunks evenly across shards in the cluster.

You can also specify the minimum number of chunks to create initially when
sharding an empty collection with a hashed shard key using the Atlas UI or by
setting the `numInitialChunks` parameter through the API.

## Note

If you specify the number of chunks per shard, Atlas creates at least the
minimum number of chunks that you specified, with the same number of chunks
per location code. If you specify the minimum number of chunks, Atlas sets up
zoned sharding quickly, especially if you already know how to geographically
distribute your data before sharding.

### Error Handling

If Atlas encounters an error while sharding a collection for global writes, a
message appears in the banner at the top of the screen.

  1. Click See Details to learn about the error and the namespace where the error occured. A modal window appears with the complete error message and a Fix Now button.

  2. Click Close and navigate to the collection in the Atlas UI. You can also click the Fix Now button to go to the Atlas UI for that Atlas cluster.

  3. Click the Global Writes tab for the collection mentioned in the error message.

  4. Click Unmanage Collection to cancel the global writes sharding operation. You must have the `Project Data Access Admin` role to cancel the sharding operation.

After you make any necessary changes to the collection as indicated by the
error message, you can start the sharding process again.

Possible errors include:

An index already exists on the custom shard key.

    If the field chosen as the second part of the compound shard key is already indexed, the sharding operation may fail.
The shard key field is not present.

    All documents in the collection must contain both the shard key fields. This error occurs only in versions earlier than MongoDB 4.4.
The collection is already sharded.

    If the collection has already been manually sharded, the operation fails.
The collection has a custom default collation.

    A custom default collation on the collection may cause a sharding error.

#### Global Cluster Write Operations

For each document in a write operation, MongoDB uses the `location` field of
the shard key (if included) to determine the zone to route the data to.
MongoDB selects a shard associated to that zone as the target for writing the
document, facilitating geographically isolated and segmented data storage.

## Warning

If a shard key isn't included in the write operation, or a shard key is
included, but the `location` field isn't present, the write operation will
succeed, but the resulting documents will not to be distributed.

MongoDB can guarantee this behavior only for inserted documents that meet the
criteria defined in Sharding Collections for Global Writes. Specifically,
MongoDB can route a document whose `location` field doesn't conform to
ISO-3166-1 alpha 2 _or_ ISO-3166-2 to any shard in the cluster.

#### Global Cluster Read Operations

MongoDB query routing depends on whether the read operation includes the full
shard key **and** that the `location` value corresponds to a supported
ISO-3166-1 alpha 2 country code (`"US"`, `"DE"`, `"IN"`) _or_ a supported
ISO-3166-2 subdivision code (`"US-DC"`, `"DE-BE"`, `"IN-DL"`).

  * For queries that do include the full shard key and whose `location` value meets the requirements for Global Writes, MongoDB targets the read operation to the zone that maps to the `location` value or values specified in the query.

  * For read operations that don't include the `location` value , or if the `location` value doesn't correspond to a supported ISO-3166-1 alpha 2 country code or ISO-3166-2 subdivision code, MongoDB must broadcast the read operation to every zone in the cluster.

  * For Global Writes zones that have Read-only nodes in geographically distant regions, clients in those regions can query the local Read-only node for that zone by specifying the full shard key as part of the query _and_ issuing the read operation with a Read Preference of `nearest`.

## Important

Secondary reads might return stale data depending on the level of replication
lag between the secondary node and the primary.

## Tip

### See also:

To learn more about:

  * MongoDB read preference, see Read Preference.

  * MongoDB query routing, see mongos.

### Sharding Collections without Global Writes

Global Writes clusters support the same Ranged and Hashed sharding strategies
as a standard Atlas sharded cluster. For sharded collections whose shard keys
and document schema don't support Global Writes, MongoDB distributes the
sharded data evenly across the available shards in the cluster with respect to
the chosen shard key. Consider using a separate sharded cluster for data that
can't take advantage of Global Writes.

You can't modify a collection to support Global Writes after sharding. We
recommend that you choose a shard key that will allow you to use Global Writes
for a collection in the future.

## Tip

### See also:

To learn more about Global Writes sharding requirements, see Sharding
Collections for Global Writes.

### Unsharded Collections in Global Write Clusters

Global Clusters provide the same support for unsharded collections as a
standard Atlas sharded cluster. For each database in the cluster, MongoDB
stores its unsharded collections on a primary shard. Use `sh.status()` from
`mongosh` to determine the primary shard for the database.

← Manage Global ClustersMove a Cluster to a Different Region →

