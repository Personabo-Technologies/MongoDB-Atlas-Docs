Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# FAQ: Deployment

Share Feedback

On this page

  * MongoDB Atlas or MongoDB Cloud Manager?
  * Can I bring an existing MongoDB deployment into MongoDB Atlas for management?
  * Can I migrate between regions?
  * Does Atlas support cross-region deployments?
  * What AWS regions does Atlas support?
  * Can I pause or stop my Atlas clusters?
  * Can I pre-split chunks in a Atlas sharded cluster?
  * Can MongoDB Atlas deploy clusters with more than 50 shards?
  * How does MongoDB Atlas deliver high availability?
  * What are Analytics Nodes?
  * Why can't I submit another disk storage change request?

## MongoDB Atlas or MongoDB Cloud Manager?

Atlas offers a managed and simplified experience. Atlas users have access to a
curated selection of configuration and infrastructure options. The available
Atlas configuration and infrastructure options may not provide the flexibility
that some users require. For example, Atlas requires TLS for cluster
connectivity and does not surface options for disabling TLS. Atlas suits users
who want fewer moving parts to manage, enabling developers and database
administrators to be more productive.

MongoDB Cloud Manager offers more control by exposing more configuration
options on the infrastructure of your choice. Cloud Manager users have access
to advanced operations and a higher level of control, but must manage the full
lifecycle of their infrastructure. Cloud Manager is best suited for users who
require a higher level of control over their MongoDB clusters.

For guidance on which MongoDB service best suits the needs of your
organization, contact MongoDB Support.

## Can I bring an existing MongoDB deployment into MongoDB Atlas for
management?

No. However, you can upload data from existing MongoDB deployment into MongoDB
Atlas.

  * You can use the Live Migrate feature in Atlas to migrate from a source replica set to an Atlas replica set cluster.

  * You can use the Live Migrate feature in Atlas to migrate from a source sharded cluster to an Atlas sharded cluster.

  * You can use `mongomirror` to migrate data from an existing MongoDB replica set into MongoDB Atlas.

  * You can use `mongodump` and `mongorestore` to seed MongoDB Atlas clusters from an existing standalone, replica set, and sharded cluster.

To learn more, see Migrate or Import Data.

You can also write scripts using official MongoDB supported drivers to upload
data.

## Can I migrate between regions?

Yes. You can change one or more regions for a given cluster within the
original cloud service provider for that cluster. Using a rolling-migration
strategy for moving nodes from the original region to a new region, MongoDB
Atlas preserves cluster availability.

## Important

### AWS Only

Amazon Web Services (AWS) Virtual Private Cloud (VPC) peering connections are
region-specific. Clusters utilizing an existing VPC peering connection to an
AWS VPC in a given AWS region lose access to that peering connection if moved
to a different AWS region. The moved cluster may use an existing peering
connection in the new region.

## Tip

### See also:

Set Up a Network Peering Connection.

If you need to migrate data between regions on different cloud service
providers, you can:

  * Perform live migration, or

  * Migrate using mongomirror, or

  * Seed the destination cluster using mongorestore, or

  * Restore a backup from the source cluster to the destination cluster.

## Tip

### See also:

Migrate or Import Data

## Does Atlas support cross-region deployments?

Yes. You can specify additional regions for high availability or local reads
when creating or scaling a deployment.

Atlas supports cross-cloud service provider deployments. To learn more, see
Electable Nodes for High Availability.

## What AWS regions does Atlas support?

Atlas supports all AWS regions other than those in China and US GovCloud. To
learn more, see Amazon Web Services (AWS).

## Can I pause or stop my Atlas clusters?

You can pause an `M10+` paid cluster for up to 30 days at a time. Atlas
automatically resumes the cluster after 30 days.

## Can I pre-split chunks in a Atlas sharded cluster?

The `Atlas admin` database user role has the necessary privileges to pre-split
chunks in an empty sharded collection.

To learn more about sharded cluster chunk creation and management, see Create
Chunks in a Sharded Cluster.

## Can MongoDB Atlas deploy clusters with more than 50 shards?

While MongoDB Atlas out of the box allows selection of up to 50 shards,
customers interested in more than 50 shards should inquire with MongoDB.
Contact MongoDB Support.

## How does MongoDB Atlas deliver high availability?

Atlas clusters use MongoDB's replication capability to deliver high
availability. All Atlas clusters are either replica sets or sharded clusters
where each shard is a replica set. For complete documentation on MongoDB
replica sets and replication, see Replication.

Atlas uses a rolling upgrade strategy for executing maintenance or
infrastructure operations, such as applying security patches or scaling up a
Atlas cluster. The rolling upgrade strategy ensures that the cluster can
process reads and writes for the majority of the maintenance or infrastructure
operation. During the rolling upgrade procedure:

  * Atlas applies the changes to each secondary node in the cluster.

  * Atlas directs the primary node to step down to the secondary state and trigger an election of a new primary.

  * Once the cluster has a new primary, Atlas applies the changes to the former primary node.

Applications must hold write operations while the cluster elects a new
primary. The cluster can continue to process secondary read operations during
this period. Elections on Atlas clusters typically complete within a few
seconds. Factors such as network latency may extend the time required for
replica set elections to complete, which in turn affects the amount of time
your cluster may operate without a primary. These factors are dependent on
your particular cluster architecture.

You can enable retryable writes by adding retryWrites=true to your Atlas URI
connection string. To learn more, see Retryable Writes.

For `M10+` clusters, Atlas provides a Test Primary Failover feature that
allows you to check that your applications can detect and react to a replica
set election. By designing applications that can seamlessly handle a replica
set election, you no longer have to worry about the underlying maintenance
occurring on your clusters.

Atlas maintenance operations include OS patches and maintenance patches for
the MongoDB database itself, such as v4.2.3 to v4.2.4. Infrastructure
operations include repair operations required to replace faulty
infrastructure, and scheduled infrastructure replacements, such as changing
the cluster tier.

Contact MongoDB Support for help with architecting your application to use
MongoDB Atlas with optimal availability.

## What are Analytics Nodes?

 _Available on M10+ clusters._

Analytics nodes are specialized read-only nodes used to isolate queries which
you do not want to affect your operational workload. They are useful for
handling analytic data such as reporting queries executed by BI tools.

Analytics nodes and read-only nodes are configured with distinct replica set
tags that allow you to direct queries to desired node types and regions. For
details on the pre-defined replica set tags implemented by Atlas, see Atlas
Replica Set Tags.

You can have up to 50 total nodes on a multi-region cluster. Within that limit
there's no maximum number of analytics nodes.

Analytics nodes cannot contribute to a cluster's availability because they
cannot participate in elections, or become the primary for their cluster.

## Why can't I submit another disk storage change request?

If you recently submitted a disk storage change request, AWS requires you to
wait 6 hours and for the first request to complete before submitting another
disk change request.

← FAQ: DatabaseFAQ: Monitoring and Alerts →

