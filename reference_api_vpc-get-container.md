Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get a Specific Network Peering Container

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

Retrieve details for one Network Peering container in an Atlas project. You
must have the `Project Read Only` or a more permissive role to successfully
call this endpoint.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/containers/{CONTAINER-ID}  
      
  
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

Unique identifier for the Atlas project whose Network Peering container
details you want to retrieve.  
  
`CONTAINER-ID`

|

string

|

Required

|

Unique identifier for the Network Peering container.  
  
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

Response Element

|

Type

|

Description  
  
||  
  
`atlasCidrBlock`

|

string

|

CIDR block that Atlas uses for your clusters.  
  
`id`

|

string

|

Unique identifier of the container.  
  
`providerName`

|

string

|

Cloud provider for this Network Peering container.  
  
`provisioned`

|

boolean

|

Flag that indicates if the project has clusters deployed in the Network
Peering container.  
  
`regionName`

|

string

|

AWS region where the VCP resides.  
  
`vpcId`

|

string

|

Unique identifier of the project's Network Peering container.  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794dee37132bb7b/containers/1112222b3bf99403840e8934?pretty=true"  
  
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

