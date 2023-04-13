Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Network Peering Connection in a Project

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

Retrieve information about one network peering connection in an Atlas project.
You must have the `Project Read Only` or more permissive role to successfully
call this endpoint.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/peers/{PEER-ID}  
      
  
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

Atlas assigned unique ID for the peering connection.

## Note

This is separate from the peering container ID. Use the Get All Peering
Connections API to retrieve a list of peering connection ids for an Atlas
project.  
  
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

This endpoint doesn't use HTTP request body parameters.

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

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|   --header "Accept: application/json" \  
    3|   --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794dee37132bb7b/peers/1112222b3bf99403840e8934?pretty=true"  
  
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

