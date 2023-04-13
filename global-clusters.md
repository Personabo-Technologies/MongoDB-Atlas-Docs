Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Global Clusters

Share Feedback

On this page

  * Global Write Zones and Zone Mapping
  * Shard Distribution
  * Configure Zone Mappings
  * Considerations

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

Use the following resources to configure and manage your Global Clusters. For
general cluster configuration, see Manage Clusters.

Atlas Global Clusters require that you define single or multi-region Zones,
where each zone supports write and read operations from geographically local
shards. You can also configure zones that support global low-latency secondary
reads. To learn more about Global Cluster zones and how to configure them, see
Global Write Zones and Zone Mapping.

## Note

Atlas does not auto-configure or auto-shard collections. You can shard global
collections for global writes. To use Global Writes, sharded collections must
meet specific compatibility requirements. To learn more, see Global Cluster
Sharding Reference.

## Global Write Zones and Zone Mapping

Each Atlas Global Cluster supports up to nine distinct zones. Each zone
consists of one Highest Priority region and one or more Electable, Read-only,
or Analytics regions. The available regions depend on the selected cloud
service provider.

Region Type

|

Description  
  
|  
  
Highest Priority

|

Region where Atlas deploys the primary replica set member for the shard or
shards associated with that zone. Clients can issue only write operations to
the primary.

Atlas uses the geographic location of the Highest Priority regions to
construct a map of geographically-near countries and subdivisions. The Global
Writes cluster uses this map for directing write operations to the correct
zone.

## Tip

To facilitate low-latency local secondary reads of globally distributed data,
for each zone in the cluster, add a Read-only node in the Highest Priority
region of every other cluster zone.  
  
Electable

|

Region where Atlas deploys the electable secondary replica set members for the
shard or shards associated to that zone. Electable regions add additional
fault tolerance in the event of a partial or total regional outage in the
Highest Priority region.  
  
Read-only

|

Region where Atlas deploys the non-electable secondary replica set members for
supporting secondary read operations.  
  
Analytics

|

Region where Atlas deploys analytics nodes. Analytics nodes are read-only
nodes configured with distinct replica set tags. You can use these tags to
direct queries to specific regions. As a result, analytics nodes can help
isolate reporting queries from your normal operational workload as well as
reduce latency for local reads.  
  
### Shard Distribution

For each shard associated to a zone, Atlas distributes the shard nodes across
the configured regions. While Atlas allows more than one shard per zone, users
should instead consider creating additional zones to address high user volume
in a concentrated geographic area.

## Note

Atlas supports up to 50 shards per sharded cluster regardless of the number of
zones. If you have requirements for more shards in your Global Cluster, click
Support from the Atlas UI to contact support.

The Atlas cluster builder includes templates for automatically configuring
Global Writes zones for the Global Cluster. Each template provides a visual
description of the cluster zone configuration, including estimates of
geographic latency and coverage.

### Configure Zone Mappings

Before you can configure zone mappings for a Global Cluster, you must create a
Global Cluster.

To configure your existing Global Cluster:

  1. Click the ellipses ... icon for the cluster you want to modify.

  2. Select Edit Configuration.

  3. In the dialog box that appears, complete the steps to configure your zones.

### Considerations

If you are using the standard connection string format rather than the DNS
seedlist format, removing an entire zone from an existing global cluster may
result in a new connection string.

To verify the correct connection string after deploying the changes:

  1. Click Databases in the top-left corner of Atlas.

  2. Click Connect from the Database Deployments view.

← Terminate a Serverless InstanceShard a Global Collection →

