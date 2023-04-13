Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# FAQ: Networking

Share Feedback

On this page

  * Do Atlas clusters' public IPs ever change?
  * Can I specify my own VPC for my MongoDB Atlas project?
  * How do I find my Atlas-side hostnames to open up my outbound firewall?
  * How many cross-region network permissions does Atlas support?
  * Can Atlas be used with AWS Transit Gateway?
  * Can Atlas be used with AWS Direct Connect?

## Do Atlas clusters' public IPs ever change?

## Note

This section applies to `M10` or larger clusters only unless specified.

An Atlas cluster's public IP addresses must change when you:

  * Vertically scale an NVMe-backed cluster on Amazon Web Services (AWS) or a cluster from any tier on Microsoft Azure within the first 12 hours of its deployment.

  * Convert a replica set to a sharded cluster.

  * Add shards to a sharded cluster.

  * Change the region(s) into which a cluster is deployed.

  * Scale an `M0`, `M2`, or `M5` cluster to an `M10` or larger cluster.

  * Terminate then re-deploy a cluster with the same name _but in a different tier_ within 36 hours.

An Atlas cluster's public IPs don't change when you:

  * Vertically scale a cluster on Amazon Web Services (AWS) that is not backed by an NVMe SSD or a cluster from any tier on Google Cloud Platform (GCP).

  * Unpause the cluster.

  * Change the cluster's topology.

  * Terminate then re-deploy a cluster with a lifetime of 12 hours or more within 12-36 hours. To learn more, see Terminate One Cluster.

  * Experience a maintenance event on your cluster.

  * Experience healing event on your cluster.

To find the public IP address for any node in your cluster, use the `nslookup`
tool from the command line. The IP address shown are the `Address` portion of
the output.

    
    
    $ nslookup ds-shard-00-00-17jcm.mongodb-dev.net  
      
      
    Address: 34.226.104.79  
  
## Can I specify my own VPC for my MongoDB Atlas project?

No. An Atlas project, and its clusters, are associated with a region-specific
VPC.

Atlas creates a VPC when you deploy the first `M10+` dedicated paid cluster to
a given provider and region. For multi-region clusters, Atlas creates one VPC
per region if there is not already a VPC for that region.

 _(AWS deployments only)_ Atlas also creates a VPC when you create a VPC
peering connection to an AWS VPC. Atlas creates the VPC in the same region as
the peered VPC.

To use a different VPC (that is, on the customer's own cloud infrastructure
accounts), you would need to use MongoDB Cloud Manager or Ops Manager.

## How do I find my Atlas-side hostnames to open up my outbound firewall?

If your firewall blocks outbound network connections, you must open outbound
access from your application environment to MongoDB Atlas. To configure your
application-side networks to accept Atlas traffic you can either use the:

  * API endpoint to retrieve the `mongoURIs` of your clusters from the response elements.

  * API endpoint to retrieve the `hostnames` of your clusters from the response elements.

You can parse these hostname values and pass the IP addresses programmatically
into your application-tier orchestration automation to push firewall updates.

To find the public IP address for any node in your cluster, use the `nslookup`
tool from the command line. The IP address is shown in the `Address` portion
of the output.

    
    
    $ nslookup ds-shard-00-00-17jcm.mongodb-dev.net  
      
      
    Address: 34.226.104.79  
  
## How many cross-region network permissions does Atlas support?

Clusters can span regions and cloud service providers. The total number of
nodes in clusters spanning across regions has a specific constraint on a per-
project basis.

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

If you would exceed the cross-region permissions limit when creating a cluster
through the Atlas Administration API, the API returns the following error:

    
    
    {  
      
      "error" : 403,  
      "detail" : "Cannot have more than 40 cross-region network permissions.",  
      "reason" : "Forbidden"  
    }  
  
## Can Atlas be used with AWS Transit Gateway?

Yes. AWS PrivateLink powers Atlas Private Endpoints. This allows for
transitive connectivity. You can use the AWS Transit Gateway with your VPC if
you connected your VPC to Atlas via AWS PrivateLink.

## Can Atlas be used with AWS Direct Connect?

Yes. AWS PrivateLink powers Atlas Private Endpoints. This allows for
transitive connectivity. You can use AWS Direct Connect with your VPC if you
connected your VPC to Atlas via AWS PrivateLink.

← FAQ: Monitoring and AlertsFAQ: Security →

