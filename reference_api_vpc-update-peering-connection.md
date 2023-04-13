Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update One New Network Peering Connection

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

Update one network peering connection in an Atlas project. You must have
either the `Project Owner` or `Organization Owner` role to successfully call
this endpoint.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    PATCH /groups/{GROUP-ID}/peers/{PEER-ID}  
      
  
### Request Path Parameters

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`GROUP-ID`

|

string

|

Required

|

Unique identifier for the project.  
  
`PEER-ID`

|

string

|

Required

|

Unique identifier for the peering connection.  
  
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
  
`accepterRegionName`

|

string

|

Required

|

Specifies the region where the peer VPC resides. For complete lists of
supported regions, see Amazon Web Services.  
  
`awsAccountId`

|

string

|

Required

|

Account ID of the owner of the peer VPC.  
  
`containerId`

|

string

|

Required

|

Unique identifier of the Atlas VPC container for the region.

You can create an Atlas network peering container using the Create Container
endpoint. You cannot create more than one container per region.

To retrieve a list of container IDs, use the Get list of VPC containers
endpoint.  
  
`providerName`

|

string

|

Optional

|

Cloud provider for this VPC peering connection. If omitted, Atlas sets this
parameter to `AWS`.  
  
`routeTableCidrBlock`

|

string

|

Required

|

Peer VPC CIDR block or subnet.  
  
`vpcId`

|

string

|

Required

|

Unique identifier of the peer VPC.  
  
## Response Elements

AWS

Azure

GCP

Body Parameter

|

Type

|

Description  
  
||  
  
`accepterRegionName`

|

string

|

AWS region where the peer VPC resides. Returns `null` if the region is the
same region in which the Atlas VPC resides.  
  
`awsAccountId`

|

string

|

AWS account ID of the owner of the peer VPC.  
  
`connectionId`

|

string

|

Unique identifier for the peering connection.  
  
`containerId`

|

string

|

Unique identifier of the Atlas VPC container for the AWS region.  
  
`errorStateName`

|

string

|

Error state, if any.

The VPC peering connection error state value can be one of the following:

  * `REJECTED`

  * `EXPIRED`

  * `INVALID_ARGUMENT`

  
  
`id`

|

string

|

CIDR block that Atlas uses for the clusters in your project.  
  
`routeTableCidrBlock`

|

string

|

Peer VPC CIDR block or subnet.  
  
`statusName`

|

string

|

The VPC peering connection status value can be one of the following:

  * `INITIATING`

  * `PENDING_ACCEPTANCE`

  * `FAILED`

  * `FINALIZING`

  * `AVAILABLE`

  * `TERMINATING`

  
  
`vpcId`

|

string

|

Unique identifier of the peer VPC.  
  
## Example Request

AWS

Azure

GCP

    
    
    1| curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
    |  
    2|  --header "Accept: application/json" \  
    3|  --header "Content-Type: application/json" \  
    4|  --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794dee37132bb7b/peers/95792d1a28f9c1c076958ef6?pretty=true" \  
    5|  --data '  
    6|    {  
    7|      "accepterRegionName" : "us-west-1",  
    8|      "awsAccountId" : "abc123abc123",  
    9|      "containerId" : "507f1f77bcf86cd799439011",  
    10|      "providerName" : "AWS",  
    11|      "routeTableCidrBlock" : "192.168.0.0/24",  
    12|      "vpcId" : "vpc-abc123abc123"  
    13|    }'  
  
## Example Response

AWS

Azure

GCP

    
    
    1| {  
    |  
    2|   "accepterRegionName" : "us-west-1",  
    3|   "awsAccountId" : "999900000000",  
    4|   "connectionId" : null,  
    5|   "containerId" : "507f1f77bcf86cd799439011",  
    6|   "errorStateName" : null,  
    7|   "id" : "1112222b3bf99403840e8934",  
    8|   "routeTableCidrBlock" : "10.15.0.0/16",  
    9|   "statusName" : "INITIATING",  
    10|   "vpcId" : "vpc-abc123abc123"  
    11| }  
  
What is MongoDB Atlas? →

