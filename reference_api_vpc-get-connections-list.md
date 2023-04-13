Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Network Peering Connections in A Project

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Retrieve details for all network peering connections in one Atlas project. You
must have the `Project Read Only` or more permissive role to successfully call
this endpoint.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/peers  
      
  
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
  
### Request Query Parameters

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
  
pageNum

|

integer

|

Optional

|

Page number, starting with one, that Atlas returns of the total number of
objects.

|

`1`  
  
itemsPerPage

|

integer

|

Optional

|

Number of items that Atlas returns per page, up to a maximum of 500.

|

`100`  
  
includeCount

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the **totalCount** parameter in the
response body.

|

`true`  
  
pretty

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the JSON response in the prettyprint
format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag that indicates whether Atlas wraps the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

Endpoints that return a list of results use the **results** object as an
envelope. Atlas adds the **status** parameter to the response body.

|

`false`  
  
|

|

|

|  
  
||||  
  
providerName

|

string

|

Optional

|

Cloud provider for this VPC peering connection. Accepted values are `AWS`,
`GCP` and `Azure`.

|

`AWS`  
  
### Request Body Parameters

This endpoint doesn't use HTTP request body parameters.

## Response Elements

### Response Document

The response JSON document includes an array of **result** objects, an array
of **link** objects and a count of the total number of **result** objects
retrieved.

Name

|

Type

|

Description  
  
||  
  
results

|

array of objects

|

One object for each item detailed in the results Embedded Document section.  
  
links

|

array of objects

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
totalCount

|

integer

|

Count of the total number of items in the result set. It may be greater than
the number of objects in the **results** array if the entire result set is
paginated.  
  
### results Embedded Document

Each element in the `result` array represents one Network Peering connection
and contains the following fields:

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

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|   --header "Accept: application/json" \  
    3|   --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794dee37132bb7b/peers?providerName=AWS&pretty=true"  
  
## Example Response

AWS

Azure

GCP

    
    
    1| {  
    |  
    2|    "links": [ {  
    3|       "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794dee37132bb7b/peers?pageNum=1&itemsPerPage=100",  
    4|       "rel" : "self"  
    5|    } ],  
    6|    "results":[ {  
    7|       "accepterRegionName" : "us-west-1",  
    8|       "awsAccountId" : "999900000000",  
    9|       "connectionId" : null,  
    10|       "containerId" : "507f1f77bcf86cd799439011",  
    11|       "errorStateName" : null,  
    12|       "id" : "1112222b3bf99403840e8934",  
    13|       "routeTableCidrBlock" : "10.15.0.0/16",  
    14|       "statusName" : "INITIATING",  
    15|       "vpcId" : "vpc-abc123abc123"  
    16|    } ],  
    17|    "totalCount": 1  
    18| }  
  
What is MongoDB Atlas? →

