Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# FAQ: Connection String Options

Share Feedback

On this page

  * Why does my cluster have multiple connection strings?
  * What does this mean for Google Cloud or Azure clusters in peering-only mode?
  * Can my VNet-peered Azure cluster span multiple regions?
  * How do I disable peering-only mode?
  * How does this affect AWS VPC peering when I use custom DNS?
  * How do I identify which connection string my application uses?
  * Do I have to update my connection string when migrating to a different cloud provider from a `M0`, `M2`, or `M5` cluster to another?
  * Do I have to update my connection string when migrating to a different cloud provider from a dedicated cluster to another?

Atlas provides multiple connection strings. These strings allow you to connect
to your clusters from both public and private contexts.

## Why does my cluster have multiple connection strings?

To connect to Atlas, point your applications to a URI to communicate with a
cluster. Atlas creates clusters with more than one node or host. Each node has
its own hostname that resolves to an IP address. The URI, known as a
_connection string_ , to which Atlas connects might have more than one
hostname. Configure Atlas to accept connections to the cluster hosts from
allowed IP addresses.

Atlas secures connections from public IP address through authentication and
TLS. If you want to connect to private IP addresses, you can use:

  * AWS and GCP VPC Peering

  * Azure VNet Peering

  * AWS PrivateLink and Azure Private Link

These features all manage communication over internal IP addresses within
secure networks.

Atlas provides more than one connection string when using secure networks.
Each network offers a string that resolves to different IP addresses.

All clusters have a standard connection string. This resolves to the
cluster's:

  * Public IP addresses for Internet connections and

  * VPC private IP addresses for AWS clusters when resolved from a peered VPC.

Use this string for applications connecting over the Internet or connecting to
peered clusters in AWS.

Clusters with peered networks have a Private IP for Peering connection string.
This string resolves to IP addresses available to:

  * Peered networks in Azure or Google Cloud

  * AWS peered clusters with a custom DNS service.

Use this connection string with applications connecting:

  * Within an Azure or Google Cloud peered network

  * To AWS clusters when using AWS with custom DNS service.

AWS or Azure clusters in regions with private endpoints configured have one or
more connection strings. Each string resolves to the private IP address of a
network interface in your VPC or VNet that connects directly to a load
balancer in the Atlas VPC or VNet. Use these connection strings with
applications connecting with private endpoints.

## What does this mean for Google Cloud or Azure clusters in peering-only
mode?

Before 31 March 2020, you were required to enable peering-only mode to connect
to databases on peer networked Azure or Google Cloud clusters. This mode:

  * Affected global DNS resolution and

  * Limited any database connections outside the peered network.

Multiple horizons lifts these restrictions and unlocks the following
additional features:

  * App Services

  * Charts

  * Live Migration

To leverage multiple horizons:

  * Update your application's existing connection strings to use Private IP for Peering connection strings,

  * Disable Peering-Only mode, and

  * Connect using the strings outlined in Why does my cluster have multiple connection strings?.

## Note

You _can_ keep connecting to your clusters using existing peering-enabled
connection strings at this time. Peering-Only mode prevents access to the
improved functionality and reduced limitations of multiple horizons. To use
the new features and remove the legacy limitations, MongoDB requires that you
use the new connection strings.

## Can my VNet-peered Azure cluster span multiple regions?

Yes.

Change your applications to connect using the Private IP for Peering
connection string. This change allows your applications to connect from peered
networks using the UI or API.

To expand into more regions, disable Peering-Only mode on existing Azure
clusters first.

## How do I disable peering-only mode?

To disable Peering-Only mode using the:

Atlas Console

Atlas Administration API

1

### Verify all clusters in your project use MongoDB 4.2 or later.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

  1. Click Database in the top-left corner of Atlas.

  2. Check the Version number under the cluster name in each cluster card on the Database Deployments page.

  3. For each cluster that doesn't run MongoDB 4.2 or later, upgrade the MongoDB version of that cluster.

2

### Update All Applications to Use Private IP for Peering Connection Strings.

Change any URLs in your applications that use your Atlas clusters to use
Private IP for Peering connection strings.

3

### Navigate to the Settings page for your project.

  1. Next to the Projects menu, expand the Options menu.

  2. Click Project Settings.

4

### Disable Connect via Peering Only.

Toggle Connect via Peering Only (GCP and Azure) to Off.

## How does this affect AWS VPC peering when I use custom DNS?

Before 31 March 2020, applications deployed within AWS using custom DNS
services and VPC-peered with Atlas couldn't connect over private IP addresses:

  * Custom DNS resolved to public IP addresses.

  * AWS internal DNS resolved to private IP addresses.

Applications deployed with custom DNS services in AWS should use Private IP
for Peering connection strings. To show these strings:

  1. Toggle the Using Custom DNS on AWS with VPC Peering on `On` from the Project Settings menu.

  2. View the connect modal for your AWS Cluster.

  3. Select the Private IP for Peering connection string.

## How do I identify which connection string my application uses?

The structure of the connection string's URI indicates the string's type. If
you have created a peering connection or private endpoint, Atlas displays more
than one of these options for your use.

### Standard Connection Strings

Standard connection strings follow this format:

    
    
    mongodb://xyz456-shard-00-00.ab123.mongodb.net:27017  
      
    mongodb+srv://xyz456.ab123.mongodb.net  
  
The dot before `ab123` _matters_. URIs using this format resolve to public IP
addresses _except_ when connecting from inside AWS with VPC-peering
configured.

## Important

This format changes one character from the Legacy Connection Strings: a hyphen
(`-`) after the cluster name becomes a period (`.`).

## Example

This _legacy connection string_ :

    
    
    mongodb+srv://xyx456-ab123.mongodb.net  
      
  
is written as this _standard connection string_ :

    
    
    mongodb+srv://xyx456.ab123.mongodb.net  
      
  
For new clusters, replica sets and shards don't derive their name from the
name of the cluster. The new names use a six alphanumeric character ID.

### Private Connection Strings

Private connection strings follow this format:

    
    
    mongodb://xyx456-shard-00-00-pri.ab123.mongodb.net:27017  
      
    mongodb+srv://xyx456-pri.ab123.mongodb.net  
  
The `-pri` before `ab123` _matters_. URIs using this format resolve to private
IP addresses reachable within the peered network. If you configure network
peering for your cluster, you must use the new hostname when you connect to
your cluster to utilize the peering.

## Important

In new clusters, replica sets and shards don't derive their name from the name
of the cluster. The new names use a six alphanumeric character ID.

### AWS Privatelink Connection Strings

AWS PrivateLink connection strings follow this format:

    
    
    mongodb://pl-0-us-east-1a.ab123.mongodb.net:1024  
      
    mongodb+srv://pl-0-us-east-1a.ab123.mongodb.net  
  
If you enable the regionalized private endpoint setting, AWS PrivateLink
connection strings follow this format:

    
    
    mongodb://pl-0-us-west-1.ab123.mongodb.net:1024  
      
    mongodb+srv://cluster0-pl-0-us-west-1.ab123.mongodb.net  
  
URIs using this format can be reachable via the AWS VPC where someone
configured PrivateLink, though access can be transitive from other VPCs peered
in turn.

### Azure Private Link Connection Strings

Azure Private Link connection strings follow this format:

    
    
    mongodb://pl-0-eastus2.ab123.azure.mongodb.net:1024  
      
    mongodb+srv://pl-0-eastus2.ab123.azure.mongodb.net  
  
If you enable the regionalized private endpoint setting, Azure Private Link
connection strings follow this format:

    
    
    mongodb://pl-0-eastus2.ab123.azure.mongodb.net:1024  
      
    mongodb+srv://cluster0-pl-0-eastus2.ab123.azure.mongodb.net  
  
URIs using this format can be reachable via the Azure VNet where someone
configured Private Link, though access can be transitive from other VNets
peered in turn.

### Legacy Connection Strings

Before 31 March 2020, you wrote Atlas connection strings as follows:

|  
  
|  
  
AWS

|

    
    
    | foo-shard-00-00-ab123.mongodb.net  
      
    foo-ab123.mongodb.net  
  
Azure

|

    
    
    | foo-shard-00-00-ab123.azure.mongodb.net  
      
    foo-ab123.azure.mongodb.net  
  
Google Cloud

|

    
    
    | foo-shard-00-00-ab123.gcp.mongodb.net  
      
    foo-ab123.gcp.mongodb.net  
  
If you enabled **Private Only** mode, these hostnames resolve to peered
network IP addresses. If you disabled that mode, hostnames resolve to public
IP addresses.

If your application uses a legacy connection string in **Peering Only** mode,
switch to Private IP for Peering connection strings.

## Do I have to update my connection string when migrating to a different
cloud provider from a `M0`, `M2`, or `M5` cluster to another?

If you have a legacy connection string and you want to change cloud providers,
your connection string must include `.gcp` or `.azure` and you want to do one
of the following:

  * Move to Google Cloud or Azure

  * Move off of Google Cloud or Azure

## Note

Either operation may change your connection string. In the Atlas UI, click
Connect on your cluster after the upgrade completes for an updated connection
string.

## Do I have to update my connection string when migrating to a different
cloud provider from a dedicated cluster to another?

It depends on the following:

  * which cloud provider your current cluster uses

  * when you created the cluster

### GCP or Azure

If you created your cluster before multi-cloud clusters were available, and
your cluster runs on Google Cloud or Azure:

  1. Open the cluster builder.

  2. Edit the cluster.

  3. Add read-only nodes from your target cloud provider.

## Note

If you are using legacy backups, keep one node in your current cloud provider,
and move the rest to your target cloud provider.

  4. Review and submit the changes.

  5. Copy the resulting comma-delimited URI connection string.

  6. Replace the connection string in your application with this new standard connection string.

This allows your application to connect to nodes from multiple cloud
providers.

  7. Restart your application.

  8. Make sure that your application can connect to Atlas.

  9. After the first change completes, reconfigure your cluster:

    * Remove all electable nodes using the original cloud provider.

    * Remove the read-only nodes for the target cloud provider.

    * Add the same number of electable nodes using the target cloud provider.

## Note

If you are using legacy backups, wait until new backups are taken, then move
the remaining node to your target cloud provider.

  10. Review and submit the changes.

  11. Copy the resulting comma-delimited URI connection string.

  12. Replace the URI connection string in your application with this new URI connection string.

  13. Restart your application.

  14. Make sure that your application can connect to Atlas.

### AWS

If your cluster runs on AWS or runs on any provider and was created after
October 2020:

  1. Open the cluster builder.

  2. Edit the cluster.

  3. Change the cloud provider.

  4. Review and submit the changes.

← FAQ: BillingFAQ: Database →

