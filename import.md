Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Migrate or Import Data

Share Feedback

On this page

  * Tools for Migrating to Atlas
  * Additional Reference

You can bring data from existing MongoDB deployments, `JSON`, or `CSV` files
into deployments in Atlas using either:

  * live migration where Atlas assists you, or

  * tools for a self-guided migration of data from your existing deployments into Atlas.

## Tools for Migrating to Atlas

The following table discusses how to choose between different tools for data
migration and import for common cluster configurations.

Source Cluster Configuration

|

Import Strategy  
  
|  
  
A MongoDB deployment that is managed by Cloud Manager or Ops Manager.

|

Use live migration (push) where Cloud Manager or Ops Manager **pushes** data
to Atlas using a secure link-token without requiring access to the source
cluster through the cluster's firewall.  
  
A MongoDB deployment that is not managed by Cloud Manager or Ops Manager.

|

Use live migration (pull) where Atlas **pulls** data from the source
deployment and requires access to the source deployment through the
deployment's firewall.  
  
A shared multi-tenant cluster, or a cluster where you have no access to the
oplog, or a cluster that runs a MongoDB version that is no longer supported.

|

Use mongorestore.  
  
A standard "single shard" sharded cluster MongoDB deployment in Compose.

|

Migrate from Compose to MongoDB Atlas.  
  
A replica set in AWS.

|

Migrate a MongoDB Replica Set from AWS to MongoDB Atlas.  
  
## Additional Reference

  * To move data to a serverless instance, use Compass to export and import data, or migrate data with self-managed tools. To learn more, see Serverless Instance Limitations.

  * To load data into a new cluster in Atlas, see Load Sample Data.

  * To make a copy of your cluster for testing purposes, see MongoDB Backup Methods.

  * If the application that you want to migrate requires a near-continuous uptime, contact MongoDB Support and share your uptime requirements and cluster configuration.

← Configure MongoDB Support Access to Atlas Backend InfrastructureLive
Migrate: Push Your Data from Cloud Manager or Ops Manager to Atlas →

