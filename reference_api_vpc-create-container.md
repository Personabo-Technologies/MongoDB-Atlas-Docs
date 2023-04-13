Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a New Network Peering Container

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Creates one Network Peering container into which Atlas can deploy Network
Peering connections.

The following table outlines the maximum number of Network Peering containers
per cloud provider:

Cloud Provider

|

Container Limit  
  
|  
  
GCP

|

One container per project.  
  
AWS and Azure

|

One container per cloud provider region.  
  
You must have either the `Project Owner` or `Organization Owner` role to
successfully call this endpoint.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    POST /groups/{GROUP-ID}/containers  
      
  
### Request Path Parameters

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
GROUP-ID

|

string

|

Required

|

Unique identifier for the Atlas project whose Network Peering container
details you want to retrieve.  
  
### Request Query Parameters

This endpoint might use any of the HTTP request query parameters available to
all Atlas Administration API resources. All of these are optional.

Name

|

Type

|

Necessity

|

Description

|

Default  
  
||||  
  
pretty

|

boolean

|

Optional

|

Flag indicating whether the response body should be in a prettyprint format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag indicating if Atlas should wrap the response in a JSON envelope.

This option may be needed for some API clients. These clients cannot access
the HTTP response headers or status code. To remediate this, set
**envelope=true** in the query.

For endpoints that return one result, the response body includes:

|

|  
  
|  
  
status

|

HTTP response code  
  
envelope

|

Expected response body  
  
`false`  
  
### Request Body Parameters

AWS

Azure

GCP

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
atlasCidrBlock

|

string

|

Required

|

CIDR block that Atlas uses for the network peering containers in your project.

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
  
providerName

|

string

|

Optional

|

Cloud provider for this Network Peering connection. If omitted, Atlas sets
this parameter to **AWS**.  
  
regionName

|

string

|

Required

|

Atlas region where the container resides.

North America

Europe

South America

Asia

Australia

Middle East

Africa

|

Region Value

|

Corresponding Region in Console  
  
|  
  
US_EAST_1

|

  1. Virginia (us-east-1)

  
  
US_EAST_2

|

Ohio (us-east-2)  
  
US_WEST_1

|

  1. California (us-west-1)

  
  
US_WEST_2

|

Oregon (us-west-2)  
  
CA_CENTRAL_1

|

Montreal (ca-central-1)  
  
### Response Elements

AWS

Azure

GCP

Field

|

Type

|

Description  
  
||  
  
atlasCidrBlock

|

string

|

CIDR block that Atlas uses for your clusters.  
  
id

|

string

|

Unique identifier of the Network Peering container.  
  
provisioned

|

boolean

|

Flag that indicates whether the project has Network Peering connections
deployed in the container.  
  
regionName

|

string

|

Region. Provided for AWS VPCs only.  
  
vpcId

|

string

|

Unique identifier of the project's VPC.  
  
## Example Request

AWS

Azure

GCP

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794dee37132bb7b/containers?pretty=true" \  
    5|      --data '  
    6|        {  
    7|          "atlasCidrBlock" : "10.8.0.0/21",  
    8|          "providerName" : "AWS",  
    9|          "regionName" : "US_EAST_1"  
    10|        }'  
  
## Example Response

AWS

Azure

GCP

    
    
    1| {  
    |  
    2|   "atlasCidrBlock" : "10.8.0.0/21",  
    3|   "id" : "1112269b3bf99403840e8934",  
    4|   "provisioned" : true,  
    5|   "regionName" : "US_EAST_1",  
    6|   "vpcId" : "vpc-zz0zzzzz"  
    7| }  
  
What is MongoDB Atlas? →

