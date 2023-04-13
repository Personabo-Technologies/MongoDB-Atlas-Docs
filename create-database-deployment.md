Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Database Deployment

Share Feedback

On this page

  * Choose a Database Deployment Type
  * Take the Next Steps

Use these resources to choose and create clusters and serverless instances.

## Choose a Database Deployment Type

MongoDB Atlas can deploy two types of cloud databases: serverless instances
and clusters. You can use both clusters and serverless instances in the same
Atlas project.

### Clusters

Create a cluster if you want to:

  * Choose a specific database configuration based on your workload requirements.

  * Define database scaling behavior.

  * Run high-throughput production workloads.

  * Always have capacity available.

You can:

  * Set the cluster tier.

  * Use advanced capabilities such as sharding.

  * Distribute your data to multiple regions and cloud providers.

  * Scale your cluster on-demand.

  * Enable autoscaling. Unlike serverless instances, autoscaling for clusters requires preconfiguration.

MongoDB bills clusters based on the deployment configuration and cluster tier.

### Serverless Instances

Create a serverless instance if you want to:

  * Get started quickly with minimal database configuration.

  * Have your database scale automatically and dynamically to meet your workload.

  * Run infrequent or sparse workloads.

  * Develop or test in a cloud environment.

Atlas automatically scales the storage capacity, storage throughput, and
computing power for a serverless instance seamlessly to meet your workload
requirements. Serverless instances always run the latest MongoDB version, and
you only pay for the operations that you run.

### Global Clusters

Create a global cluster if you want to support location-aware read and write
operations. Location-aware read and write operations are ideal for globally-
distributed application instances and clients.

Global Clusters are a highly-curated implementation of a sharded cluster that
offer:

  * Low-latency read and write operations for globally distributed clients.

  * Uptime protection during partial or full regional outages.

  * Location-aware data storage in specific geographic regions.

  * Workload isolation based on cluster member types.

You can enable Global Writes in Atlas when deploying an `M30` or greater
sharded cluster. For replica sets, scale the cluster to at least an `M30` tier
and enable Global Writes. All shard nodes deploy with the selected cluster.

## Important

You can't disable Global Writes for a cluster once it is deployed.

### Feature Support and Comparison

The following table indicates whether clusters or serverless instances support
the listed configuration or capability in MongoDB Atlas.

## Note

MongoDB plans to add support for more configurations and capabilities on
serverless instances over time. To see the current serverless instance
limitations and learn about planned support, see Serverless Instance
Limitations.

For the latest product updates, see the Atlas Changelog.

#### Configurations

Configuration

|

Clusters

|

Serverless instances  
  
||  
  
Rapid releases

|

 __

|

 __  
  
AWS regions

|

 __

|

Select regions only  
  
Google Cloud regions

|

 __

|

Select regions only  
  
Microsoft Azure regions

|

 __

|

Select regions only  
  
Multi-region deployments

|

 __

|  
  
Multi-cloud deployments

|

 __

|  
  
Sharded deployments

|

 __

|  
  
Global clusters

|

 __

|  
  
IP access list

|

 __

|

 __  
  
Network peering

|

 __

|  
  
Private endpoints

|

 __

|

AWS and Azure only  
  
Advanced enterprise security features (including LDAP and database auditing)

|

 __

|  
  
#### Capabilities

Capability

|

Clusters

|

Serverless instances  
  
||  
  
Use the Atlas API

|

 __

|

 __  
  
Monitor metrics

|

 __

|

 __  
  
Configure alerts on available metrics or billing

|

 __

|

 __  
  
Configurebackups

|

 __

|

 __  
  
Performpoint-in-time or automated restores from backup snapshots

|

 __

|

 __  
  
Use theAtlas UI (Find, Indexes, Schema Advisor and Aggregation Pipeline
Builder)

|

 __

|

 __  
  
Get on-demandindex and schema suggestions

|

 __

|  
  
Load sample data

|

 __

|

 __  
  
Usetriggers

|

 __

|  
  
UseAtlas Search

|

 __

|  
  
UseOnline Archive

|

 __

|  
  
Runfederated queries

|

 __

|

 __  
  
Use BI Connector

|

 __

|  
  
Use MongoDB Charts

|

 __

|

 __  
  
Use Atlas App Services

|

 __

|

Selective Support  
  
## Important

You can’t migrate into clusters from serverless instances.

For a full list of serverless instance limitations, see Serverless Instance
Limitations.

## Take the Next Steps

Once you select a database deployment type, you can:

  * Create a cluster.

  * Create a serverless instance.

  * Create a global cluster.

← Create and Connect to Database DeploymentsCreate a Cluster →

