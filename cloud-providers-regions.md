Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Cloud Providers and Regions

Share Feedback

On this page

  * Cloud Providers and Regions for Serverless Instances
  * Cloud Providers and Regions for Shared Clusters

The choice of cloud provider and region affects network latency for clients
accessing your database deployment and the cost of running the database
deployment. For clusters, this choice also affects the configuration options
for the available cluster tiers. The region refers to the physical location of
your MongoDB database deployment.

## Cloud Providers and Regions for Serverless Instances

Atlas supports deploying serverless instances on all cloud providers but only
to a subset of each cloud provider's regions. For a list of regions that
support serverless instances, see:

  * Amazon Web Services (AWS)

  * Google Cloud Platform (GCP)

  * Microsoft Azure

## Cloud Providers and Regions for Shared Clusters

Atlas supports deploying `M0` free clusters and `M2/M5` shared clusters on all
cloud providers but only to a subset of each cloud provider's regions. For a
list of regions that support `M0` or `M2/M5` clusters, see:

  * Amazon Web Services (AWS)

  * Google Cloud Platform (GCP)

  * Microsoft Azure

In the Create New Cluster page:

  * Regions marked as ★ are Recommended regions that provide higher availability compared to other regions.

  * Regions marked as __under Shared tier are not available for shared tier clusters and therefore appear grayed-out. These regions are available for dedicated clusters only.

For more information, see:

  * AWS Recommended Regions

  * GCP Recommended Regions

  * Azure Recommended Regions

## Tip

### See also:

For more information on multi-region configurations for increased
availability, see Configure High Availability and Workload Isolation.

← Create a Global ClusterConnect to a Database Deployment →

