Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure High Availability and Workload Isolation

Share Feedback

On this page

  * Considerations
  * Electable Nodes for High Availability
  * Add Electable Nodes
  * Remove Electable Nodes
  * Change Electable Nodes to Read-Only Nodes
  * Improve the Availability of a Cluster
  * Change the Highest Priority Provider or Region
  * Read-Only Nodes for Optimal Local Reads
  * Add Read-Only Nodes
  * Remove Read-Only Nodes
  * Change Workload Purpose of Nodes
  * Analytics Nodes for Workload Isolation
  * Add Analytics Nodes
  * Select a Cluster Tier for Your Analytics Nodes
  * Remove Analytics Nodes
  * Limitations

## Tip

You can create multi-cloud MongoDB deployments in Atlas using any combination
of cloud providers: AWS, Azure, and Google Cloud.

You can set the nodes in your MongoDB deployment to use different:

  * Cloud providers

  * Geographic regions

  * Workload priorities

  * Replication configurations

Using these options allows you to improve the availability and workload
balancing of your cluster.

To configure node-specific options for your cluster, toggle Multi-Cloud,
Multi-Region & Workload Isolation (M10+ clusters) to On.

click to enlarge

A cluster may be hosted in:

  * Multiple regions within a single cloud provider.

  * Multiple regions across multiple cloud providers.

As each cloud provider has its own set of regions, multi-cloud clusters are
also multi-region clusters.

## Considerations

  * Atlas does not guarantee that host names remain consistent with respect to node types during topology changes.

## Example

If you have a cluster named `foo123` containing an analytics node
`foo123-shard-00-03-a1b2c.mongodb.net:27017`, Atlas does not guarantee that
specific host name will continue to refer to an analytics node after a
topology change, such as scaling a cluster to modify its number of nodes or
regions.

  * In sharded clusters, Atlas distributes the three config server nodes based on the number of electable regions in the cluster. If the cluster has:

    * Only one electable region, Atlas deploys all three config nodes in that region.

    * Two electable regions, Atlas deploys two config nodes in the highest priority region and one config node in the second highest priority region.

    * Three or more electable regions, Atlas deploys one config node in each of the three highest priority regions.

  * Having a large number of regions or having nodes spread across long distances may lead to long election times or replication lag.

  * A cluster change that adds, removes, or modifies voting members will take longer, since Atlas adds, removes, or modifies voting members one at a time on a rolling basis.

  * Clusters can span regions and cloud service providers. The total number of nodes in clusters spanning across regions has a specific constraint on a per-project basis.

Atlas limits the total number of nodes in other regions in one project to a
total of 40. This total excludes:

    * Google Cloud regions communicating with each other

    * Free clusters or shared clusters

The total number of nodes between any two regions must meet this constraint.

## Example

If an Atlas project has nodes in clusters spread across three regions:

    * 30 nodes in **Region A**

    * 10 nodes in **Region B**

    * 5 nodes in **Region C**

You can only add 5 more nodes to **Region C** because:

    1. If you exclude Region C, Region A + Region B = 40. __

    2. If you exclude Region B, Region A + Region C = 35, <= 40. __

    3. If you exclude Region A, Region B + Region C = 15, <= 40. __

    4. Each combination of regions with the added 5 nodes still meets the per-project constraint:

      * Region A + B = 40 __

      * Region A + C = 40 __

      * Region B + C = 20 __

You can't create a multi-region cluster in a project if it has one or more
clusters spanning 40 or more nodes in other regions.

Contact Atlas support for questions or assistance with raising this limit.

  * Atlas provides built-in custom write concerns for multi-region clusters. Use these write concerns to ensure your write operations propagate to a desired number of regions, thereby ensuring data consistency across your regions. To learn more, see Built-In Custom Write Concerns.

  * The number of availability zones, zones, or fault domains in a region has no effect on the number of MongoDB nodes Atlas can deploy. MongoDB Atlas clusters are always made of replica sets with a minimum of three MongoDB nodes.

  * If you use the standard connection string format rather than the DNS seedlist format, removing an entire region from an existing cross-region cluster may result in a new connection string.

To verify the correct connection string after deploying the changes:

    1. Click Database in the top-left corner of Atlas.

    2. Click Connect from the Database Deployments view.

  * If you plan on creating one or more VPC peering connections on your first `M10+` dedicated paid cluster for the selected region or regions, first review the documentation on VPC Peering Connections.

## Electable Nodes for High Availability

If you add regions with electable nodes, you:

  * increase data availability and

  * reduce the impact of data center outages.

You may set different regions from one cloud provider or choose different
cloud providers.

Atlas sets the node in the first row of the Electable nodes table as the
Highest Priority region.

Atlas prioritizes nodes in this region for primary eligibility. Other nodes
rank in the order that they appear. For more information, see Member Priority.

Each electable node can:

  * Participate in replica set elections.

  * Become the primary while the majority of nodes in the replica set remain available.

### Add Electable Nodes

You can add electable nodes in one cloud provider and region from the
Electable nodes for high availability section.

To add an electable node:

  1. Click Add a provider/region.

  2. Select the cloud provider from the Provider dropdown.

  3. Select the region from the Region dropdown.

When you change the Provider option, the Region changes to a blank option. If
you don't select a region, Atlas displays an error when you click Create
Cluster.

  4. Specify the desired number of Nodes for the provider and region.

The total number of electable nodes across all providers and regions in the
cluster must equal **3** , **5** , or **7**.

Atlas considers regions marked with a __as recommended. These regions provide
higher availability compared to other regions.

## Tip

### See also:

  * AWS Recommended Regions

  * GCP Recommended Regions

  * Azure Recommended Regions

### Remove Electable Nodes

To remove a node from a region, click the __icon to the right side of that
region. You cannot remove a node in the Highest Priority region.

## Tip

### See also:

Multi-Region Cluster Backups

### Change Electable Nodes to Read-Only Nodes

You can change an electable node to a read-only node by adding a read-only
node and removing an electable node at the same time. To learn more, see
Change Workload Purpose of Nodes.

### Improve the Availability of a Cluster

To improve the redundancy and availability of a cluster, increase the number
of electable nodes in that region. Every Atlas cluster has a Highest Priority
region. If your cluster spans multiple regions, you can select which cloud
provider region should be the Highest Priority.

To prevent loss of availability and performance, consider the following
scenarios:

Point of Failure

|

How to Prevent this Point of Failure  
  
|  
  
Cloud Provider

|

Minimum of one node set in all three cloud providers. More than one node per
region.  
  
Region

|

Minimum of one node set in three or more different regions. More than one node
per region.  
  
Node

|

  * Three or more electable nodes in a Recommended region _or_

  * Three or more electable nodes across two or more regions.

  
  
### Change the Highest Priority Provider or Region

If you change the Highest Priority provider and region in an active multi-
region cluster, Atlas selects a new primary node in the provider and region
that you specify (assuming that the number of nodes in each provider and
region remains the same and nothing else is modified).

## Example

If you have an active 5-node cluster with the following configuration:

Nodes

|

Provider

|

Region

|

Priority  
  
|||  
  
3

|

AWS

|

 **us-east-1**

|

Highest  
  
2

|

Google Cloud

|

 **us-west3**

|  
  
To make the Google Cloud **us-west3** nodes the Highest Priority, drag its row
to the top of your cluster's Electable nodes list. After this change, Atlas
elects a new **PRIMARY** in **us-west3**. Atlas doesn't start an initial sync
or re-provision hosts when changing this configuration.

## Important

Certain circumstances may delay an election of a new primary.

## Example

A sharded cluster with heavy workloads on its primary shard may delay the
election. This results in not having all primary nodes in the same region
temporarily.

To minimize these risks, avoid modifying your primary region during periods of
heavy workload.

## Read-Only Nodes for Optimal Local Reads

Use read-only nodes to optimize local reads in the nodes' respective service
areas.

### Add Read-Only Nodes

You can add read-only nodes from the Read-Only Nodes for Optimal Local Reads
section.

To add a read-only node in one cloud provider and region:

  1. Click Add a provider/region.

  2. Select the cloud provider from the Provider dropdown.

  3. Select the region from the Region dropdown.

When you change the Provider option, the Region changes to a blank option. If
you don't select a region, Atlas displays an error when you click Create
Cluster.

  4. Specify the desired number of Nodes for the provider and region.

Atlas considers regions marked with a __as recommended. These regions provide
higher availability compared to other regions.

Read-only nodes don't provide high availability because they don't participate
in elections. They can't become the primary for their cluster. Read-only nodes
have distinct read preference tags that allow you to direct queries to desired
regions.

### Remove Read-Only Nodes

To remove all read-only nodes in one cloud provider and region, click the
__icon to the right of that cloud provider and region.

### Change Workload Purpose of Nodes

You can change a node's workload purpose by adding and removing nodes at the
same time.

## Note

You must add and remove the node within the same configuration change to reuse
a node. If you remove the node, save the change, then add the node, Atlas
provisions a new node instead.

For example, to change a read-only node to an electable node:

  1. Add an electable node.

  2. Remove a read-only node.

  3. Click Review Changes.

  4. Click Apply Changes.

## Analytics Nodes for Workload Isolation

Use analytics nodes to isolate queries which you do not wish to contend with
your operational workload. Analytics nodes help handle data analysis
operations, such as reporting queries from BI Connector for Atlas. Analytics
nodes have distinct replica set tags which allow you to direct queries to
desired regions.

Click Add a region to select a region in which to deploy analytics nodes.
Specify the desired number of Nodes for the region.

## Note

The readPreference and readPreferenceTags connection string options are
unavailable for the mongo shell. See cursor.readPref() and Mongo.setReadPref()
instead.

### Add Analytics Nodes

You can add analytics nodes from the Analytics nodes for workload isolation
section.

To add analytics nodes in one cloud provider and region:

  1. Click Add a provider/region.

  2. Select the cloud provider from the Provider dropdown.

  3. Select the region from the Region dropdown.

When you change the Provider option, the Region changes to a blank option. If
you don't select a region, Atlas displays an error when you click Create
Cluster.

  4. Specify the desired number of Nodes for the provider and region.

Atlas considers regions marked with a __as recommended. These regions provide
higher availability compared to other regions.

Analytics nodes don't provide high availability because they don't participate
in elections. They can't become the primary for their cluster.

### Select a Cluster Tier for Your Analytics Nodes

Your workloads can vary greatly between analytics and operational nodes. To
help manage this issue, for `M10+` clusters, you can select a cluster tier
appropriately sized for your analytics workload. You can select a cluster tier
for your analytics nodes that's larger or smaller than the cluster tier
selected for your electable and read-only nodes (operational nodes). This
functionality helps to ensure that you get the performance required for your
transactional and analytical queries without over or under provisioning your
entire cluster for your analytical workload.

The following considerations apply to the Analytics Tier tab and analytic
nodes:

## Important

If you select a cluster tier on the Analytics Tier tab significantly below the
cluster tier selected on the Base Tier tab, replication lag might result. The
analytics node might fall off the oplog altogether.

  * If you select a General cluster tier on the Analytics Tier tab and a Low-CPU cluster tier on the Base Tier tab, disk auto-scaling isn't supported for the cluster. Disk auto-scaling also isn't supported if you select a General cluster tier on the Base Tier tab and a Low-CPU cluster tier on the Analytics Tier tab.

  * Disk size and IOPS must remain the same across all node types.

  * Storage size must match between the Base Tier tab and Analytics Tier tab. You can set the storage size on the Base Tier tab.

  * If you want to select the Local NVME SSD class on the Base Tier tab, the Analytics Tier tab must have the same tier level selected.

  * If a cluster tier appears grayed out, the cluster tier isn't compatible with the disk size of the cluster or the Local NVME SSD class.

  * A cluster tier selected on the Analytics Tier tab is priced the same as a cluster tier selected on the Base Tier tab. However, when an Analytics Tier is higher or lower than the Base Tier, the price adjusts accordingly on a prorated per-node basis. The pricing appears in the Atlas UI when you create or edit a cluster. To learn more, see, Manage Billing.

After you add your analytics nodes, you can select a cluster tier
appropriately sized for your analytics workload.

  1. In the Cluster Tier section, click the Analytics Tier tab.

  2. Select the Cluster Tier.

### Remove Analytics Nodes

To remove all analytics nodes in one cloud provider and region, click the
__icon to the right of that cloud provider and region.

## Limitations

If you're connecting to a multi-cloud deployment through a private connection,
you can access only the nodes in the same cloud provider that you're
connecting from. This cloud provider might not have the primary node in its
region. When this happens, you must specify the secondary read preference mode
in the connection string to access the deployment.

If you need access to all nodes for your multi-cloud deployment from your
current provider through a private connection, you must:

  * Configure a VPN in the current provider to each of the remaining providers.

  * Configure a private endpoint to Atlas for each of the remaining providers.

← Pause, Resume, or Terminate a ClusterQuery using Replica Set Tags →

