Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Convert a Shared Cluster to a Serverless Instance

Share Feedback

On this page

  * Considerations
  * Prerequisites
  * Convert Your Shared Cluster

You can edit the database deployment configuration in the Atlas UI to convert
a shared cluster (`M0`, `M2`, or `M5`) to a serverless instance. When you
convert a shared cluster to a serverless instance, you can also change the
cloud provider, region, and backup options.

To learn more about the use cases for clusters and serverless instances and
determine which is best for you, see Create a Database Deployment.

Atlas doesn't support conversion from a dedicated cluster to a serverless
instance.

## Important

### A serverless instance can't convert to a cluster

You can't convert a serverless instance back to a cluster. To move your data
back to a cluster, you must manually migrate to a new cluster of the same
MongoDB version as your serverless instance using mongodump and mongorestore.
If the serverless instance runs on a rapid release version of MongoDB, you
can't migrate to a shared cluster. To learn more, see the Operational
Considerations.

Read the considerations carefully before you proceed with the conversion to a
serverless instance.

## Considerations

Consider the following factors before you convert a shared cluster to a
serverless instance:

### Limitations

Serverless instances don't support the same features as shared clusters. If
you change your shared cluster to a serverless instance, you lose access to
the following features.

MongoDB plans to add support for more configurations and capabilities on
serverless instances over time. To learn which features MongoDB plans to
support for serverless instances in the future, see Serverless Instance
Limitations.

Configuration/Operation

|

Notes  
  
|  
  
Select Cloud Service Provider Regions

|

You can deploy both shared clusters and serverless instances in a subset of
regions on AWS, Google Cloud, and Azure, but serverless instances support
fewer regions across all cloud service providers. To learn more about the
supported cloud provider regions for each database deployment type, see:

  * Amazon Web Services (AWS)

  * Google Cloud Platform (GCP)

  * Microsoft Azure

If your current cloud provider region is unsupported for serverless instances,
Atlas alerts you before conversion and lets you choose a new cloud provider
and region.  
  
Select Driver Version Support

|

Some driver versions that shared clusters support are unsupported for
serverless instances. If you connect to Atlas using a driver, check the
Minimum Driver Versions for Serverless Instances.  
  
To see the full list of limitations for serverless instances, see Serverless
Instance Limitations. Atlas supports some features listed in the Serverless
Instance Limitations only for dedicated clusters, so the features might be
unsupported for your current shared cluster tier.

### Compatibility

  * You can't convert a shared cluster to a serverless instance if you connected the cluster to any of the following:

    * Atlas App Services

    * Atlas Search

You must disconnect the shared cluster from these features before you convert
to a serverless instance.

## Note

You can convert your shared cluster to a serverless instance 15-20 minutes
after you disconnect it from Atlas App Services and Atlas Search.

  * You can't convert a cluster that contains a capped collection to a serverless instance.

  * You can't convert a cluster to a serverless instance if you use collation on the cluster's collections, indexes, or queries.

  * You can't convert a paused `M0` cluster to a serverless instance. You must resume the paused cluster before you change it to a serverless instance.

### Operational Considerations

  * Shared clusters always follow a major release cadence. Serverless instances always run on the latest MongoDB release, which may be a rapid release. Atlas automatically upgrades to the latest MongoDB version when you convert to a serverless instance, but you should:

    * Ensure that the latest MongoDB version is compatible with your application.

    * Consider that you can't reverse conversion to a serverless instance. To revert to using a cluster after you convert to a serverless instance, you must use mongodump and mongorestore to manually migrate your data to a new cluster.

mongodump and mongorestore support migration only between database deployments
of the same MongoDB version. As a result, if the MongoDB version of the
serverless instance is later than all available major versions for shared
clusters, you can migrate only to a dedicated cluster until the next major
version release.

To learn more about release cadences, see Choosing a Release Cadence.

  * You can connect to a serverless instance only using a DNS seed list connection string. If you use a different connection string format to connect to your shared cluster, change your connection string after you convert to a serverless instance. To learn more and find your connection string, see Connect to Your Database Deployment.

  * If you use MongoDB Charts, all existing charts that use this cluster won't render until you update the data source to the respective collection in the new serverless instance.

### Downtime During Conversion

Your database deployment must go offline while it converts to a serverless
instance. As a result:

  * You can't read/write to the database deployment while Atlas converts a shared cluster to a serverless instance.

  * Atlas doesn't preserve sessions, transactions, retryable writes, and change streams from before the conversion.

### Billing Considerations

  * Serverless instances offer pay-per-operation pricing. You pay only for the Processing Units consumed by your database operations and storage consumed by your data and indexes. To learn more, see Serverless Instance Costs.

  * Atlas selects Serverless Continuous Backup by default when you convert a shared cluster to a serverless instance. To learn about the costs associated with continuous backup, see the Continuous Backup row of the Usage Cost Summary in Serverless Instance Costs.

## Prerequisites

Before you convert to a serverless instance, disconnect your shared cluster
from Atlas App Services and Atlas Search:

  * To disconnect your cluster from Atlas App Services, you must unlink the cluster as a data source from all of your apps. To learn more, see Update an App.

  * To disconnect your cluster from Atlas Search, you must delete all Atlas Search indexes for your cluster. To learn more, see Delete an Atlas Search Index.

## Convert Your Shared Cluster

After you complete the prerequisites, to convert your shared cluster to a
serverless instance:

1

Click the __next to the name of your shared cluster and select Edit
Configuration.

2

### Click Serverless.

3

### (Optional) Change the cloud provider and region.

If your current cloud provider region is unsupported for serverless instances,
Atlas alerts you and chooses the default region for your cloud provider. You
can select another cloud provider and region or accept the default selections.

If your current cloud provider region is supported, the Cloud Provider &
Region section is collapsed. You can expand the section and select another
cloud provider and region.

4

### (Optional) Change the backup options.

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
  
Atlas selects Serverless Continuous Backup by default. To change to Basic
Backup, expand the Backup section and select Basic Backup.

5

### Read and acknowledge the considerations.

Check the box next to I understand and agree to the considerations of
converting to a serverless instance.

6

### Click Review Changes.

7

### Review the changes and click Apply Changes.

You can use a DNS seed list connection string to connect to your new
serverless instance.

← Modify a ClusterReconfigure a Replica Set During a Regional Outage →

