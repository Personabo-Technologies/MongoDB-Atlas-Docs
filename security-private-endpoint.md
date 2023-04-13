Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up a Private Endpoint

Share Feedback

On this page

  * Overview
  * Considerations
  * High Availability
  * Port Ranges Used for Private Endpoints
  * Private Endpoint-Aware Connection Strings
  * Limitations
  * Prerequisites
  * Procedures
  * Configure an Atlas Private Endpoint
  * Connect to Atlas using a Private Endpoint
  * View Private Endpoints
  * Remove a Private Endpoint from Atlas
  * Troubleshoot Private Endpoint Connection Issues
  * Check the status of your AWS PrivateLink connections.
  * Make sure that your security groups are configured properly.
  * Check the status of your AWS PrivateLink connections.
  * Make sure that your security groups are configured properly.

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

## Overview

MongoDB Atlas supports private endpoints on dedicated clusters and serverless
instances. Select your database deployment type to learn which cloud providers
Atlas supports:

Dedicated Clusters

Serverless Instances

  * AWS using the AWS PrivateLink feature.

  * Azure using the Azure Private Link feature.

  * Google Cloud using the Private Service Connect feature.

You can also set up private endpoints for your Online Archive. To learn more,
see Set Up a Private Endpoint for Online Archives.

AWS PrivateLink

Azure Private Link

Private Service Connect

When you enable this feature, Atlas creates its own VPC and places database
deployments within a region behind a network load balancer in the Atlas VPC.

Then you create resources that establish a one-way connection from your VPC to
the network load balancer in the Atlas VPC using a private endpoint.

AWS PrivateLink

AWS PrivateLink with Direct Connect

click to enlarge

Connections to Atlas database deployments using private endpoints offer the
following advantages over other network access management options:

  * Connections using private endpoints are one-way. Atlas VPCs can't initiate connections back to your VPCs. This ensures your perceived network trust boundary is not extended.

  * Connections to private endpoints within your VPC can be made transitively from:

    * Another VPC peered to the private endpoint-connected VPC.

    * An on-premises data center connected with DirectConnect to the private endpoint-connected VPC. This enables you to connect to Atlas directly from your on-premises data center without adding public IP addresses to the Atlas IP access list.

## Considerations

### High Availability

Dedicated Clusters

Serverless Instances

AWS PrivateLink

Azure Private Link

Private Service Connect

To ensure private endpoint connections to Atlas can withstand an availability
zone outage, you should deploy subnets to multiple availability zones in a
region.

### Port Ranges Used for Private Endpoints

Dedicated Clusters

Serverless Instances

AWS PrivateLink

Azure Private Link

Private Service Connect

AWS PrivateLink supports 50 addressable targets, Atlas can use port 1024
through port 65535, but typically starts with port 1024. The ports can change
under specific circumstances, including (but not limited to) cluster changes.

## Important

MongoDB strongly recommends using the DNS seedlist private endpoint-aware
connection string, so that DNS automatically updates the ports that AWS
PrivateLink uses if they change. For the same reason, MongoDB also strongly
recommends allow-listing the entire port range, instead of specific ports.

### Private Endpoint-Aware Connection Strings

Dedicated Clusters

Serverless Instances

AWS PrivateLink

Azure Private Link

Private Service Connect

Dedicated Clusters

Serverless Instances

When you configure a private endpoint, Atlas generates DNS seedlist and
standard private endpoint-aware connection strings:

  * DNS seedlist connection
    
        mongodb+srv://cluster0-pl-0-k45tj.mongodb.net  
      
  
  * Standard connection string
    
        mongodb://pl-0-us-east-1-k45tj.mongodb.net:1024,pl-0-us-east-1-k45tj.mongodb.net:1025,pl-0-us-east-1-k45tj.mongodb.net:1026/?ssl=true&authSource=admin&replicaSet=Cluster0-shard-0-shard-0  
      
  

When a client in your VPC connects to an Atlas database deployment using one
of these private endpoint-aware connection strings, the client attempts to
establish a connection to the load balancer in the Atlas VPC through one of
the interface endpoints. Your client's DNS resolution mechanism handles which
of the interface endpoints the hostname resolves to. If one interface endpoint
is unavailable the next is used. This is opaque to the driver or other
connection mechanism. The driver is only aware of the hostname in the SRV
record or in the connection string.

 **SRV Record for DNS Seedlist Private Endpoint-Aware Connection Strings**

The following example shows the SRV record for an AWS PrivateLink -enabled
single-region cluster, showing three unique ports defined for `pl-0-us-
east-1-k45tj.mongodb.net`:

    
    
    $ nslookup -type=SRV _mongodb._tcp.cluster0-pl-0-k45tj.mongodb.net  
      
      
    Server: 127.0.0.53  
    Address: 127.0.0.53#53  
      
    Non-authoritative answer:  
    _mongodb._tcp.cluster0-pl-0-k45tj.mongodb.net service = 0 0 1026 pl-0-us-east-1-k45tj.mongodb.net.  
    _mongodb._tcp.cluster0-pl-0-k45tj.mongodb.net service = 0 0 1024 pl-0-us-east-1-k45tj.mongodb.net.  
    _mongodb._tcp.cluster0-pl-0-k45tj.mongodb.net service = 0 0 1025 pl-0-us-east-1-k45tj.mongodb.net.  
  
## Tip

In the preceding example:

  * `_mongodb._tcp.cluster0-pl-0-k45tj.mongodb.net` is the SRV record that the `mongodb+srv://cluster0-pl-0-k45tj.mongodb.net` connection string references.

  * `pl-0-us-east-1-k45tj.mongodb.net` is the hostname for each node in one Atlas cluster in one region for which you have configured AWS PrivateLink.

  * `1024`, `1025`, and `1026` are unique ports that Atlas assigns on the load balancer for each Atlas replica set node in the region for which you enabled AWS PrivateLink. All nodes in an Atlas replica set are accessible via the same hostname, with the load balancer resolving individual nodes by their unique port.

 **Hostname DNS Resolution in Private Endpoint-Aware Connection Strings and
SRV Records**

The hostname in the SRV record and the standard connection string is a DNS
Canonical Name (`CNAME`) record that resolves to the endpoint-specific
regional DNS name that AWS generates for the interface endpoint. A DNS `ALIAS`
record exists for each subnet in your VPC that you deployed the interface
endpoint to. Each `ALIAS` record contains the private IP address of the
interface endpoint for that subnet.

The following example shows the DNS lookup for the hostname in the SRV record
and in the standard connection string, including the endpoint-specific
regional DNS name for the interface endpoint and its DNS `ALIAS` records:

    
    
    $ nslookup pl-0-us-east-1-k45tj.mongodb.net  
      
    Server: 127.0.0.53  
    Address: 127.0.0.53#53  
      
    Non-authoritative answer:  
    pl-0-us-east-1-k45tj.mongodb.net  
    canonical name = vpce-024f5b57108c8d3ed-ypwbxwll.vpce-svc-02863655456245e5c.us-east-1.vpce.amazonaws.com.  
      
    Name: vpce-024f5b57108c8d3ed-ypwbxwll.vpce-svc-02863655456245e5c.us-east-1.vpce.amazonaws.com  
    Address: 10.0.30.194  
    Name: vpce-024f5b57108c8d3ed-ypwbxwll.vpce-svc-02863655456245e5c.us-east-1.vpce.amazonaws.com  
    Address: 10.0.20.54  
  
## Tip

### See also:

Connect to Atlas using a Private Endpoint

Dedicated Clusters

Serverless Instances

#### IP Access Lists and Network Peering Connections with Private Endpoints

When you enable private endpoints, you can still enable access to your Atlas
database deployments using other methods, such as adding public IPs to IP
access lists and network peering.

Clients connecting to Atlas database deployments using other methods use
standard connection strings. Your clients might have to identify when to use
private endpoint-aware connection strings and standard connection strings.

#### (Optional) Regionalized Private Endpoints for Multi-Region Sharded
Clusters

For multi-region and global sharded clusters, you can deploy multiple private
endpoints to a region if you need to connect to Atlas using a private endpoint
from networks that can't be peered with one another.

You can deploy any number of private endpoints to regions that you deployed
your database deployment to. Each regional private endpoint connects to the
`mongos` instances in that region.

## Warning

Your connection strings to existing multi-region and global sharded clusters
change when you enable this setting.

You must update your applications to use the new connection strings. This
might cause downtime.

You can enable this setting only if your Atlas project contains no replica
sets.

You can't disable this setting if you have:

  * More than one private endpoint in more than one region, or

  * More than one private endpoint in one region and one private endpoint in one or more regions.

You can create only sharded clusters when you enable the regionalized private
endpoint setting. You can't create replica sets.

To use this feature, you must enable the regionalized private endpoint
setting.

To enable or disable the regionalized private endpoint setting:

Atlas CLI

Atlas UI

##### Enable Regionalized Private Endpoints

To enable the regionalized private endpoint setting for your project using the
Atlas CLI, run the following command:

    
    
    atlas privateEndpoints regionalModes enable [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints regionalModes enable.

##### Disable Regionalized Private Endpoints

To disable the regionalized private endpoint setting for your project using
the Atlas CLI, run the following command:

    
    
    atlas privateEndpoints regionalModes disable [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints regionalModes disable.

##### View Regionalized Private Endpoint Settings

To return the regionalized private endpoint settings for your project using
the Atlas CLI, run the following command:

    
    
    atlas privateEndpoints regionalModes describe [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints regionalModes describe.

##### (Optional) Improve Connection Performance for Sharded Clusters Behind a
Private Endpoint

Atlas can generate an optimized SRV connection string for sharded clusters
using the load balancers from your private endpoint service. When you use an
optimized connection string, Atlas limits the number of connections per
`mongos` between your application and your sharded cluster. The limited
connections per `mongos` improve performance during spikes in connection
counts.

## Note

Atlas doesn't support optimized connection strings for clusters that run on
Google Cloud or Azure.

To learn more about optimized connection strings for sharded clusters behind a
private endpoint, see Improve Connection Performance for Sharded Clusters
Behind a Private Endpoint.

## Limitations

Dedicated Clusters

Serverless Instances

AWS PrivateLink

Azure Private Link

Private Service Connect

  * AWS PrivateLink must be active in all regions into which you deploy a multi-region cluster. You will receive an error if AWS PrivateLink is active in some, but not all, targeted regions. If you have a multi-cloud cluster in AWS or Azure, you must provision an endpoint in each provider or region.

  * You can do only one of the following:

    * Create more than one private endpoint in a single region.

    * Create no more than one private endpoint per region, if nodes are deployed in more than one region.

## Important

This limitation applies across cloud providers. For example, if you create
more than one private endpoint in a single region in AWS, you can't create
private endpoints in more than one region in Azure.

See (Optional) Regionalized Private Endpoints for Multi-Region Sharded
Clusters for an exception for multi-region and global sharded clusters.

  * To connect to Atlas database deployments using AWS PrivateLink from regions in which you haven't deployed a private endpoint connection, you must peer VPCs in those regions to VPCs in a region in which you have deployed a private endpoint connection.

To learn about inter-region VPC peering, see the AWS documentation.

  * You can use AWS PrivateLink in Atlas projects with up to 50 addressable targets **per region**. If you need more than 50 addressable targets in a region:

    * Contact MongoDB Support, or

    * Use additional projects or regions to connect to addressable targets beyond this limit.

Addressable targets include:

    * Each `mongod` instance in a replica set deployment (sharded clusters excluded).

    * Each sharded cluster deployment that use optimized connection strings.

    * Each `mongos` instance for sharded cluster deployments that use non-optimized connection strings.

    * Each BI Connector for Atlas instance across all dedicated clusters in the project.

## Note

To request a one-time increase to use AWS PrivateLink with up to 100
addressable targets per Atlas project, contact MongoDB Support.

  * If this is the first private endpoint that you deploy to a region, you must first resume any paused database deployments in your project with nodes deployed to that region. This limitation doesn't apply for additional private endpoints that you deploy to the same region.

## Prerequisites

To enable connections to Atlas using private endpoints, you must:

  * Have a valid payment method already configured for your organization.

Dedicated Clusters

Serverless Instances

AWS PrivateLink

Azure Private Link

Private Service Connect

  * Have either the `Project Owner` or `Organization Owner` role in Atlas.

  * Have an AWS user account with an IAM user policy that grants permissions to create, modify, describe, and delete endpoints. For more information on controlling the use of interface endpoints, see the AWS Documentation.

  *  **(Recommended)** : Install the AWS CLI.

  * If you have not already done so, create your VPC and EC2 instances in AWS. See the AWS documentation for guidance.

## Procedures

### Configure an Atlas Private Endpoint

Use these resources to configure an Atlas private endpoint:

  * Set Up a Private Endpoint for a Dedicated Cluster

  * Set Up a Private Endpoint for a Serverless Instance

#### Private Endpoint Configuration Atlas CLI Commands

## Note

For step-by-step instructions on configuring a private endpoint using the
Atlas CLI, see the Atlas CLI tab on Set Up a Private Endpoint for a Dedicated
Cluster.

Dedicated Clusters

AWS PrivateLink

Azure Private Link

Private Service Connect

### Connect to Atlas using a Private Endpoint

## Note

For important considerations about private endpoint-aware connection strings,
see Private Endpoint-Aware Connection Strings.

Use a private endpoint-aware connection string to connect to an Atlas database
deployment with the following procedure:

Dedicated Clusters

Serverless Instances

1

#### Click Connect.

  1. Click Database in the top-left corner of Atlas.

  2. In the Database Deployments view, click Connect for the database deployment to which you want to connect.

2

#### Select the Private Endpoint connection type.

3

#### Select the private endpoint to which you want to connect.

4

#### Create a Database User.

## Important

 **Skip this step** if Atlas indicates in the Setup connection security step
that you have at least one database user configured in your project. To manage
existing database users, see Configure Database Users.

To access the database deployment, you need a MongoDB user with access to the
desired database or databases on the database deployment in your project. If
your project has no MongoDB users, Atlas prompts you to create a new user with
the Atlas Admin role.

  1. Enter the new user's Username.

  2. Enter a Password for this new user or click Autogenerate Secure Password.

  3. Click Create Database User to save the user.

Use this user to connect to your database deployment in the following step.

Once you have added a database user, click Choose Your Connection Method.

5

#### Click Choose a connection method.

AWS PrivateLink

Azure Private Link

Private Service Connect

Private endpoint-aware connection strings are available in one of the
following formats:

  * DNS seedlist connection
    
        mongodb+srv://cluster0-pl-0-auylw.mongodb.net  
      
  
  * Standard connection string
    
        mongodb://pl-0-us-east-1-auylw.mongodb.net:1024,pl-0-us-east-1-auylw.mongodb.net:1025,pl-0-us-east-1-auylw.mongodb.net:1026/?ssl=true&authSource=admin&replicaSet=Cluster0-shard-0-shard-0  
      
  

MongoDB recommends that your clients use the DNS seedlist connection string
format.

### View Private Endpoints

Dedicated Clusters

Serverless Instances

AWS PrivateLink

Azure Private Link

Private Service Connect

Atlas CLI

Atlas UI

#### Endpoints

To return the details of the AWS private endpoint you specify using the Atlas
CLI, run the following command:

    
    
    atlas privateEndpoints aws describe <privateEndpointId> [options]  
      
  
To list all AWS private endpoints in a project using the Atlas CLI, run the
following command:

    
    
    atlas privateEndpoints aws list [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas privateEndpoints aws describe and atlas
privateEndpoints aws list.

#### Interface Endpoints

To return the AWS private endpoint interface that you specify. using the Atlas
CLI, run the following command:

    
    
    atlas privateEndpoints aws interfaces describe <interfaceEndpointId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints aws interfaces describe.

### Remove a Private Endpoint from Atlas

Dedicated Clusters

Serverless Instances

AWS PrivateLink

Azure Private Link

Private Service Connect

Atlas CLI

Atlas UI

#### Endpoints

To delete the AWS private endpoint you specify using the Atlas CLI, run the
following command:

    
    
    atlas privateEndpoints aws delete <privateEndpointId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints aws delete.

#### Interface Endpoints

To delete the AWS private endpoint interface you specify using the Atlas CLI,
run the following command:

    
    
    atlas privateEndpoints aws interfaces delete <interfaceEndpointId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints aws interfaces delete.

## Troubleshoot Private Endpoint Connection Issues

Dedicated Clusters

Serverless Instances

AWS PrivateLink

Azure Private Link

Private Service Connect

1

### Check the status of your AWS PrivateLink connections.

The Private Endpoint tab on the Network Access page lists each private
endpoint you've created. The Atlas Endpoint Service Status and Endpoint Status
fields show the status of each private endpoint.

Refer to the following statuses to help you determine the state of your
private endpoint connections:

Atlas Endpoint Service Status

Status

|

Description  
  
|  
  
Creating private link

|

Atlas is creating the network load balancer and VPC resources.  
  
Failed

|

A system failure has occurred.  
  
Available

|

The Atlas network load balancer and VPC endpoint service are created and ready
to receive connection requests.  
  
Deleting

|

Atlas is deleting the private endpoint service.  
  
Endpoint Status

Status

|

Description  
  
|  
  
Not configured

|

Atlas created the network load balancer and VPC endpoint service, but AWS
hasn't yet created the interface endpoint. Click Edit and complete the wizard
to create the interface endpoint.  
  
Pending acceptance

|

AWS has received the connection request from your interface endpoint to the
Atlas VPC endpoint service.  
  
Pending

|

AWS is establishing the connection between your interface endpoint and the
Atlas VPC endpoint service.  
  
Failed

|

AWS failed to establish a connection between Atlas VPC resources and the
interface endpoint in your VPC. Click Edit, verify that the information you
provided is correct, and then create the private endpoint again.

## Important

If your Interface Endpoint fails, you might see the following message:

## Example

No dns entries found for endpoint vpce-<guid>, your endpoint must be
provisioned in at least one subnet Click "Edit" to fix the problem.

This message indicated that you didn't specify a subnet when you created the
AWS PrivateLink connection. To resolve this error:

  1. Click Edit.

  2. Click Back.

  3. Specify at least one subnet.

  4. Follow the remaining instructions to create the AWS PrivateLink connection.

  
  
Available

|

Atlas VPC resources are connected to the interface endpoint in your VPC. You
can connect to Atlas clusters in this region using AWS PrivateLink.  
  
Deleting

|

Atlas is removing the interface endpoint from the private endpoint service.  
  
2

### Make sure that your security groups are configured properly.

  1. For each resource that needs to connect to your Atlas clusters using AWS PrivateLink, the resource's security group must allow outbound traffic to the interface endpoint's private IP(s) on all ports.

See Adding Rules to a Security Group for more information.

  2. Your interface endpoint security group must allow inbound traffic on all ports from each resource that needs to connect to your Atlas clusters using AWS PrivateLink.

Whitelist instance IP addresses or security groups to allow traffic from them
to reach the interface endpoint security group.

← Set Up a Network Peering ConnectionSet Up a Private Endpoint for a Dedicated
Cluster →

