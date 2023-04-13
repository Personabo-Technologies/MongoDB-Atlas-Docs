Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Cluster

Share Feedback

This tutorial takes you through the steps to create a new Atlas cluster. To
learn how to modify an existing Atlas cluster, see Modify a Cluster.

Clusters can be either a replica set or a sharded cluster. This tutorial walks
you through creating a replica set.

## Considerations

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

  * Each Atlas project supports up to 25 database deployments. Please contact Atlas support for questions or assistance regarding the database deployment limit. To contact support, select Support from the left-hand navigation bar of the Atlas UI.

  * If your Atlas project contains a custom role that uses actions introduced in a specific MongoDB version, you must delete that role before creating clusters with an earlier MongoDB version.

  * Atlas clusters created after July 2020 use TLS version 1.2 by default.

  * When you create a cluster, Atlas creates a network container in the project for the cloud provider to which you deploy the cluster if one does not already exist.

  * If you have a Backup Compliance Policy enabled, all new and existing clusters have Cloud Backup automatically enabled and use the project-level Backup Compliance Policy. Atlas augments any preexisting cluster-level policies to meet the minimum requirements of the Backup Compliance Policy. All new clusters use the Backup Compliance Policy unless the mininum requirements of the cluster-level backup policy expand beyond the mininum requirements of the Backup Compliance Policy.

## Procedure

Atlas CLI

Atlas UI

To create one cluster in the specified project using the Atlas CLI, run the
following command:

    
    
    atlas clusters create [name] [options]  
      
  
To watch for a specific cluster to become available using the Atlas CLI, run
the following command:

    
    
    atlas clusters watch <clusterName> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas clusters create and atlas clusters
watch.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### View Available Regions

To list available regions that Atlas supports for new deployments using the
Atlas CLI, run the following command:

    
    
    atlas clusters availableRegions list [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters availableRegions list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

[1]|  _(1, 2)_ For replica sets, the data-bearing servers are the servers
hosting the replica set nodes. For sharded clusters, the data-bearing servers
are the servers hosting the shards. For sharded clusters, Atlas also deploys
servers for the config servers; these are charged at a rate separate from the
cluster costs.  
|  
  
← Create a Database DeploymentCreate a Serverless Instance →

