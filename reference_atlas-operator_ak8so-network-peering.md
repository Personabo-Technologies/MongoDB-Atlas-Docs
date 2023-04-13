Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Network Peering

Share Feedback

On this page

  * Prerequisites
  * Procedure

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

Atlas supports network peering connections for dedicated clusters hosted on
AWS, Google Cloud, and Azure, and on multi-cloud sharded clusters.

Network peering establishes a private connection between your Atlas VPC and
your cloud provider's VPC. The connection isolates traffic from public
networks for added security.

Atlas doesn't support network peering between clusters you deploy in a single
region on different cloud providers.

To manage your network peering connections with Atlas Kubernetes Operator, you
can specify and update the `spec.networkPeers` parameter for the
`AtlasProject` Custom Resource. Each time you change the `spec` field in any
of the supported custom resources, Atlas Kubernetes Operator creates or
updates the corresponding Atlas configuration.

## Prerequisites

To configure network peering using Atlas Kubernetes Operator, you require:

AWS PrivateLink

Azure Private Link

Private Service Connect

  * A running Kubernetes cluster with Atlas Kubernetes Operator deployed.

  * The `Project Owner` or `Organization Owner` role in Atlas.

  * If you have not already done so, create your VPC in AWS. To learn more, see Get Started with Amazon VPC.

  * A network traffic rule for outbound traffic.

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
  

## Procedure

Enable clients to connect to Atlas clusters using a network peering connection
with the following procedure:

AWS PrivateLink

Azure Private Link

Private Service Connect

1

### Specify the `spec.networkPeers` parameter.

You can configure network peering to use an existing container or a new
container.

#### Use an Existing Container

  1. Specify the `spec.networkPeers` parameter in the `AtlasProject` Custom Resource. Replace the following placeholders with your values:

Placeholder

|

Description  
  
|  
  
`spec.networkPeers.providerName`

|

Cloud provider name. Specify `AWS`.  
  
`spec.networkPeers.containerId`

|

Unique identifier for the network peering container you want to use. If you
don't specify `containerId`, you must set `atlasCIDRblock`. To learn more, see
the Create New Container section in this procedure.  
  
`spec.networkPeers.accepterRegionName`

|

AWS region for your VPC.  
  
`spec.networkPeers.awsAccountId`

|

Unique identifier for your AWS account. AWS displays the account ID when you
click the account name in the top right corner of the console home page.  
  
`spec.networkPeers.routeTableCidrBlock`

|

CIDR block for your AWS VPC. AWS displays the CIDR block on your VPC's details
page.  
  
`spec.networkPeers.vpcId`

|

Unique identifier for your AWS VPC. AWS displays the VPC ID on your VPC's
details page.  
  
  2. Run the following command:
    
        cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Atlas Operator Project  
      networkPeers:  
      - providerName: "AWS"  
        containerID: "6dc5f17280eef56a459fa3fb"  
        accepterRegionName: "us-east-2"  
        awsAccountId: "12345678"  
        routeTableCidrBlock: "10.0.0.0/24"  
        vpcId: "vpc-12345678"  
    EOF  
  

#### Create a New Container

  1. Specify the `spec.networkPeers` parameter in the `AtlasProject` Custom Resource. Replace the following placeholders with your values:

Placeholder

|

Description  
  
|  
  
`spec.networkPeers.providerName`

|

Cloud provider name. Specify `AWS`.  
  
`spec.networkPeers.atlasCidrBlock`

|

Atlas CIDR block for which Atlas Kubernetes Operator creates a new container.
If you don't specify `atlasCidrBlock`, you must specify the `containerId` of
an existing container. To learn more, see the Use Existing Container section
in this procedure.  
  
`spec.networkPeers.containerRegion`

|

(Optional) AWS region in which Atlas Kubernetes Operator creates a new
container. If you don't specify either a `containerRegion` or a `containerId`,
Atlas Kubernetes Operator creates a new container in the same region as the
`accepterRegionName`.  
  
`spec.networkPeers.accepterRegionName`

|

AWS region for your VPC.  
  
`spec.networkPeers.awsAccountId`

|

Unique identifier for your AWS account. AWS displays the account ID when you
click the account name in the top right corner of the console home page.  
  
`spec.networkPeers.routeTableCidrBlock`

|

CIDR block for your AWS VPC. AWS displays the CIDR block on your VPC's details
page.  
  
`spec.networkPeers.vpcId`

|

Unique identifier for your AWS VPC. AWS displays the VPC ID on your VPC's
details page.  
  
  2. Run the following command:
    
        cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Atlas Operator Project  
      networkPeers:  
      - providerName: "AWS"  
        atlasCidrBlock: "10.8.0.0/21"  
        containerRegion: "us-west-1"  
        accepterRegionName: "us-east-2"  
        awsAccountId: "12345678"  
        routeTableCidrBlock: "10.0.0.0/24"  
        vpcId: "vpc-12345678"  
    EOF  
  

2

### Check for the `WAITING FOR USER` status.

  1. Run the following command:
    
        kubectl get atlasprojects my-project -o=jsonpath='{.status.networkPeers.statusName}'  
      
  
HIDE OUTPUT

    
        WAITING FOR USER  
      
  
  2. If the `statusName` value is `WAITING FOR USER`, proceed to the next step. If the `statusName` is not `WAITING FOR USER`, wait a few minutes and try this step again.

3

### Accept the VPC peering connection in AWS.

To learn more, see Accept a VPC peering connection.

4

### Check the status of your VPC connection using Atlas Kubernetes Operator.

Run the following command again to check the status of the VPC connection.
Atlas Kubernetes Operator returns `READY` when the network peering connection
is complete.

    
    
    kubectl get atlasprojects my-project -o=jsonpath='{.status.networkPeers.statusName}'  
      
  
HIDE OUTPUT

    
    
    READY  
      
  
← Set Up X.509 AuthenticationSet Up Unified Cloud Provider Access →

