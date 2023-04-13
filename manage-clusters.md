Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Clusters

Share Feedback

On this page

  * View Your Clusters
  * Select Cluster Tier
  * Shared Clusters
  * Dedicated Clusters for Low-Traffic Applications
  * Dedicated Clusters for High-Traffic Applications
  * NVMe Storage
  * Free, Shared, and Dedicated Cluster Comparison
  * Take the Next Steps

Use the following resources to configure and manage Atlas clusters. These
settings don't apply to serverless instances.

## View Your Clusters

Atlas CLI

Atlas UI

To list all clusters for your project using the Atlas CLI, run the following
command:

    
    
    atlas clusters list [options]  
      
  
To return the details for the cluster you specify using the Atlas CLI, run the
following command:

    
    
    atlas clusters describe <clusterName> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas clusters list and atlas clusters
describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

To return the advanced configuration settings details for the cluster you
specify using the Atlas CLI, run the following command:

    
    
    atlas clusters advancedSettings describe <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters advancedSettings describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Select Cluster Tier

Select your preferred cluster tier. The cluster tier dictates the memory,
storage, and IOPS specification for each data-bearing server [1] in the
cluster.

## Note

You might see different values depending on your selected cloud provider and
region.

### Shared Clusters

Use Shared clusters as economical clusters for getting started with MongoDB
and for low-throughput applications. These clusters deploy to a shared
environment with access to a subset of Atlas features. To learn more about
shared cluster limitations, see Atlas M0 (Free Cluster), M2, and M5
Limitations.

You can deploy one `M0` cluster (free sandbox replica set cluster) per Atlas
project. You can upgrade an `M0` free cluster to an `M2+` shared cluster at
any time.

`M2` and `M5` clusters (low-cost shared clusters) provide the following added
features compared to `M0` clusters:

  * Backups for your cluster data

  * Increased storage

  * API access

#### Considerations

  * Atlas deploys MongoDB 5.0 for all shared clusters (`M0`, `M2`, and `M5`). However, Shared Clusters don't support all functionality in MongoDB version 5.0 and later. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * Atlas supports shared cluster deployment in a subset of cloud providers and regions. Atlas grays out any shared cluster tiers that the selected cloud service provider and region doesn't support. To learn more about the regions that support shared cluster deployments, see:

    * Amazon Web Services (AWS)

    * Google Cloud Platform (GCP)

    * Microsoft Azure

### Dedicated Clusters for Low-Traffic Applications

`M10` and `M20` cluster tiers support development environments and low-traffic
applications.

These clusters support replica set deployments only, but otherwise provide
full access to Atlas features.

## Note

`M10` and `M20` cluster tiers run on a burstable performance infrastructure.

### Dedicated Clusters for High-Traffic Applications

`M30+` cluster tiers support production environments with high-traffic
applications and large datasets.

These clusters support replica set and sharded cluster deployments with full
access to Atlas features.

Some clusters have variants, denoted by the ❯ character. When you select these
clusters, Atlas lists the variants and tags each cluster to distinguish their
key characteristics.

### NVMe Storage

For applications hosted on AWS or Azure that require low-latency and high-
throughput I/O, Atlas offers storage options using locally attached ephemeral
NVMe SSDs.

## Note

Atlas doesn't support NVMe clusters on Google Cloud.

#### NVMe Considerations

The following cluster tiers support NVMe clusters on AWS:

  * `M40`

  * `M50`

  * `M60`

  * `M80`

  * `M200`

  * `M400`

The following cluster tiers support NVMe clusters on Azure:

  * `M60`

  * `M80`

  * `M200`

  * `M300`

  * `M400`

  * `M600`

Atlas supports NVMe clusters in the following Azure regions:

Americas

Europe

Asia Pacific

Azure Region

|

Location

|

Atlas Region  
  
||  
  
`centralus`

|

Iowa, USA

|

`US_CENTRAL`  
  
`eastus`

|

Virginia (East US)

|

`US_EAST`  
  
`eastus2`

|

Virginia, USA

|

`US_EAST_2`  
  
`southcentralus`

|

Texas, USA

|

`US_SOUTH_CENTRAL`  
  
The fixed-value storage space and RAM for an NVMe cluster corresponds to its
cluster tier. To learn more, see Amazon Cluster Configuration Options and
Azure Cluster Configuration Options.

Clusters with NVMe storage use Cloud Backups. You can't disable backup on NVMe
clusters. If you want to use hourly backups, Atlas limits backups on NVMe
clusters to once every 12 hours.

NVMe clusters use a hidden secondary node that consists of a provisioned
volume with high throughput and IOPS to facilitate backup.

You can't pause an NVMe cluster.

## Note

NVMe clusters auto-scale to the next higher tier when 90% of the available
storage space is consumed, and the migration requires an initial sync.

##### NVMe Availability Zones

NVMe clusters in the following Azure regions have two Availability Zones:

  * `eastus2`

  * `centralus`

  * `southcentralus`

NVMe clusters in all other Azure regions that indicate Availability Zones have
three Availability Zones.

### Free, Shared, and Dedicated Cluster Comparison

The following table highlights key differences between an `M0` Free Tier
cluster, an `M2` or `M5` shared cluster, and an `M10+` dedicated cluster.

|

Free Cluster (`M0`)

|

Shared Cluster (`M2` and `M5`)

|

Dedicated Cluster (`M10` and larger)  
  
|||  
  
Storage (Data Size + Index Size)

|

512 MB

|

`M2`: 2 GB

`M5`: 5 GB

|

10 - 4000 GB  
  
MongoDB Version Support

|

5.0

|

5.0

|

4.2, 4.4, 5.0, Latest Release  
  
Metrics and Alerts

|

Limited

|

Limited

|

Full metrics, including the Real Time Performance Tab, and full alert
configuration options.  
  
VPC Peering

|

No

|

No

|

VPC Peering Connection wizard  
  
Global Region Selection

|

Atlas supports deploying `M0` clusters in a subset of regions in AWS, Google
Cloud, and Azure.

|

Atlas supports deploying `M2` and `M5` clusters in a subset of regions in AWS,
Google Cloud, and Azure.

|

Atlas supports deploying clusters globally on Amazon Web Services, Google
Cloud Platform, and Microsoft Azure  
  
Cross-Region Deployments

|

No

|

No

|

Yes. Specify additional regions for high availability or local reads when
creating or scaling a cluster.  
  
Backups

|

No

|

Yes, daily backup snapshots

|

Yes, including queryable backups  
  
Sharding

|

No

|

No

|

Yes, for clusters using an `M30+` tier  
  
Dedicated Cluster

|

No, `M0` free clusters run in a shared environment

|

No, `M2` and `M5` clusters run in a shared environment

|

Yes, `M10+` clusters deploy each `mongod` process to its own instance.  
  
Performance Advisor

|

No

|

No

|

Yes  
  
BI Connector for Atlas

|

No

|

No

|

Yes  
  
For a complete list of M0 free cluster, M2, and M5 limitations, see Atlas M0
(Free Cluster), M2, and M5 Limitations.

## Tip

### See also:

Configure Auto-Scaling

[1]|  For replica sets, the data-bearing servers are the servers hosting the
replica set nodes. For sharded clusters, the data-bearing servers are the
servers hosting the shards. For sharded clusters, Atlas also deploys servers
for the config servers; these are charged at a rate separate from the cluster
costs.  
|  
  
## Take the Next Steps

You can manage clusters in the following ways:

Action

|

Description  
  
|  
  
Customize Cluster Storage

|

Customize the storage capacity of your cluster. Each cluster tier comes with a
default set of resources. `M10+` clusters provide the ability to customize
your storage capacity.  
  
Configure Auto-Scaling

|

Configure the cluster tier ranges that Atlas uses to automatically scale your
cluster tier, storage capacity, or both in response to cluster usage.  
  
Configure Additional Settings

|

Configure additional cluster settings such as MongoDB version, backup, and
encryption options.  
  
Modify a Cluster

|

Reconfigure an existing cluster. Modify any of the available Atlas
configuration options.  
  
Upgrade Major MongoDB Version for a Cluster

|

Manage major version upgrades for your cluster. Atlas enables you to upgrade
the major version of an Atlas cluster at any time.  
  
Configure Maintenance Window

|

Configure maintenance windows for your cluster. You can set the hour of the
day that Atlas should start weekly maintenance on your cluster.  
  
Pause, Resume, or Terminate a Cluster

|

Pause, resume, or terminate an existing cluster. You can't change the
configuration of a paused cluster. Also, you can't read data from or write
data to a paused cluster.  
  
Configure High Availability and Workload Isolation

|

Configure multi-cloud distribution for increased availability. Atlas offers
options to improve the availability and workload balancing of your cluster.  
  
Query using Replica Set Tags

|

Use replica set tags to direct queries from specific applications to desired
node types and regions. To use replica set tags in your connection string and
direct queries to desired nodes, set the tag in the `readPreferenceTags`
connection string option.  
  
← Manage Database DeploymentsCustomize Cluster Storage →

