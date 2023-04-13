Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up a Network Peering Connection

Share Feedback

On this page

  * Configure Network Containers
  * Configure an Atlas Network Peering Connection
  * View Atlas Network Peering Connections
  * Remove an Atlas Network Peering Connection
  * Network Peering Architectures

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

Atlas supports network peering connections for dedicated clusters hosted on
AWS, Google Cloud, and Azure, and on multi-cloud sharded clusters.

Network peering establishes a private connection between your Atlas VPC and
your cloud provider's VPC. The connection isolates traffic from public
networks for added security.

## Warning

Atlas does not support Network Peering between clusters deployed in a single
region on different cloud providers. For example, you cannot set up Network
Peering between an Atlas cluster hosted in a single region on AWS and an
application hosted in a single region on GCP.

## Important

To set up a Network Peering connection, you must have either the `Project
Owner` or `Organization Owner` role.

## Configure Network Containers

### Create a Network Container

To configure the Atlas CIDR without configuring Network Peering, see Create a
New Network Peering Container. You must use the API to create the container
without Network Peering.

### View Network Containers

Atlas CLI

Atlas Administration API

To list all network peering containers for your project using the Atlas CLI,
run the following command:

    
    
    atlas networking containers list [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas networking containers list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Delete Network Containers

Atlas CLI

Atlas Administration API

To delete the network peering container you specify using the Atlas CLI, run
the following command:

    
    
    atlas networking containers delete <containerId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas networking containers delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Configure an Atlas Network Peering Connection

To configure Atlas Network Peering for a cluster, perform the procedure on the
tab corresponding to your cluster's cloud provider. You also configure the
Atlas VPC CIDR during this procedure.

AWS

Azure

GCP

### Considerations

#### DNS Configuration

DNS resolves the cluster's hostnames to their public IP address rather than
their internal IP address if:

  * DNS hostnames are disabled,

  * DNS resolution is disabled, and

  * The user accesses the Atlas cluster from outside a peered VPC.

To learn more about how to enable these options, see Updating DNS Support for
Your VPC.

If the applications deployed within AWS use custom DNS services and VPC
peering with Atlas, see the FAQ to learn how to connect using private
connection strings.

#### Deployments in Multiple Regions

Atlas deployments in multiple regions must have a peering connection for each
Atlas region.

For example: If you have a VPC in Sydney and Atlas deployments in Sydney and
Singapore, create two peering connections.

### AWS VPC Peering Prerequisites

Create the following network traffic rule on your AWS security group attached
to your resources that connect to Atlas:

Permission

|

Direction

|

Port

|

Target  
  
|||  
  
Allow

|

outbound

|

27015-27017 inclusive

|

to your Atlas CIDR  
  
### Configure Network Peering for an AWS-backed Cluster

To configure Atlas VPC Peering for an AWS-backed cluster:

1

#### In AWS, enable DNS hostnames and DNS resolution.

  1. Log in to your AWS account.

  2. Go to the VPC dashboard.

  3. Open your list of VPC resources.

  4. Select the VPC you want to peer with.

  5. Enable DNS hostnames and DNS resolution.

These settings ensure that when your application connects to the cluster
within the VPC it uses private IP addresses.

2

#### In Atlas, add a new network peering connection for your project.

## Note

You can skip this step if you are using the Atlas CLI to add a network peering
connection.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Network Access in the sidebar.

  4. In the Peering tab, click __ Add Peering Connection.

3

#### In Atlas, configure your network peering connection.

Atlas CLI

Atlas UI

To create a network peering connection with AWS using the Atlas CLI, run the
following command:

    
    
    atlas networking peering create aws [options]  
      
  
To watch for a peering connection to become available using the Atlas CLI, run
the following command:

    
    
    atlas networking peering watch <peerId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas networking peering create aws and atlas
networking peering watch.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

  1. Fill out the fields in the Your Atlas VPC section.

Field

|

Description  
  
|  
  
Atlas VPC Region

|

AWS region where the Atlas VPC resides. Atlas creates a VPC for the Atlas
project in your chosen region if that region has no `M10` or greater clusters
or VPC peering connections.

Clear Same as application VPC region to select a region different from where
your application's VPC resides.  
  
VPC CIDR

|

Atlas uses this Atlas CIDR block for all other Network Peering connections
created in the project. The Atlas CIDR block must be at least a `/24` and at
most a `/21` in one of the following private networks.

|

Lower Bound

|

Upper Bound

|

Prefix  
  
||  
  
`10.0.0.0`

|

`10.255.255.255`

|

`10/8`  
  
`172.16.0.0`

|

`172.31.255.255`

|

`172.16/12`  
  
`192.168.0.0`

|

`192.168.255.255`

|

`192.168/16`  
  
Atlas locks this value for a given region if an `M10` or greater cluster or a
Network Peering connection already exists in that region.

To modify the CIDR block, the target project cannot have:

    * Any `M10` or greater clusters with nodes in the target region

    * Any cloud backup snapshots stored in the target region

    * Any other VPC peering connections to the target region

You can also create a new project then create a Network Peering Connection to
set the desired Atlas VPC CIDR block for that project.

## Important

Atlas limits the number of MongoDB nodes per Network Peering connection based
on the CIDR block and the region selected for the project.

## Example

A project in an AWS region supporting 3 availability zones and a Atlas CIDR
VPC block of `/24` is limited to the equivalent of 27 three-node replica sets.

Contact MongoDB Support for any questions on Atlas limits of MongoDB nodes per
VPC.  
  
  2. Click Initiate Peering.

  3. Wait for approval of peering connection request.

The owner of the peer VPC must approve the VPC peering connection request.
Ensure that the owner approves the request.

Atlas provides instructions for approving the connection request.

## Important

### Requests expire after 7 days.

4

#### In AWS, update your VPC's route table.

  1. In the VPC Dashboard, click Route Tables.

  2. Select the Route Table for your VPC or subnet(s).

  3. Click the Routes tab.

  4. Click Edit Routes.

  5. Click Add route.

  6. Add the Atlas VPC's CIDR block to the Destination column.

  7. Add the AWS Peering Connection ID to the Target column.

This value uses a prefix of `pcx-`.

  8. Click Save.

## Note

Each Atlas project may have a maximum of 50 peering connections in total. This
total includes a maximum of 25 pending peering connections.

Once set up, you can edit or terminate VPC peering connection from the Peering
table.

Before your new VPC peer can connect to your Atlas cluster, you must:

  * Locate the VPC CIDR block addresses (or subset), or the Security Groups, associated with the VPC configured in your project.

  * Add at least one of these CIDR blocks to the access list.

## Tip

### See also:

  * CIDR Subnet Selection for MongoDB Atlas

  * FAQ on changes to AWS network peering.

## View Atlas Network Peering Connections

Atlas CLI

Atlas UI

To return the details for all network peering connections in the project you
specify using the Atlas CLI, run the following command:

    
    
    atlas networking peering list [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas networking peering list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Remove an Atlas Network Peering Connection

Atlas CLI

Atlas UI

To delete the network peering connection you specify using the Atlas CLI, run
the following command:

    
    
    atlas networking peering delete <peerId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas networking peering delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Network Peering Architectures

Multiple cloud-hosted applications might need to connect securely to the same
Atlas project.

### Network Peering between an Atlas VPC and Two Virtual Networks with
Identical CIDR Blocks

Consider a case where two applications use virtual networks (VPC, VNet) with
identical IP CIDR blocks. You want both applications to securely connect to
the same Atlas cluster via VPC peering. To achieve this, create one network
peering connection between each application's virtual network and your Atlas
cluster.

Cloud provider virtual networks can’t peer to each other if they have
identical CIDR blocks. However, you can peer each of the applications' virtual
networks with the Atlas virtual network if the Atlas virtual network includes
two non-overlapping CIDR blocks. Configure each of the peering connections to
have non-overlapping route-back CIDR blocks in the Atlas virtual network.

Follow this general process:

  1. Before you deploy any clusters, create a network peering connection for each virtual network that you want to peer with Atlas. You do this by creating a CIDR block in the Atlas virtual network for each application's virtual network.

  2. In the virtual network's configuration for your cloud provider, establish routing between each of your application's virtual networks and their respective Atlas CIDR blocks.

  3. Deploy your Atlas cluster.

← Configure IP Access List EntriesSet Up a Private Endpoint →

