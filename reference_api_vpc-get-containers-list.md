Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Network Peering Containers in One Project by Cloud Provider

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

Retrieve a list of Network Peering containers in one project for a single
cloud provider. If you do not specify the cloud provider, Atlas defaults to
Amazon Web Services (AWS). You must have the `Project Read Only` or a more
permissive role to successfully call this endpoint.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/containers  
      
  
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

Unique identifier for the project whose list of Network Peering containers you
want to retrieve.  
  
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
  
|

|

|

|  
  
||||  
  
`providerName`

|

string

|

Optional

|

Cloud provider for this Network peering container. Accepted values are `AWS`,
`GCP`, and `Azure`.

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

AWS

Azure

GCP

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|   --header "Accept: application/json" \  
    3|   --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/containers?providerName=AWS&pretty=true"  
  
## Example Response

AWS

Azure

GCP

    
    
    1| {  
    |  
    2|    "links":[ {  
    3|       "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/containers?pageNum=1&itemsPerPage=100",  
    4|       "rel" : "self"  
    5|    } ],  
    6|    "results":[ {  
    7|      "atlasCidrBlock" : "10.8.0.0/21",  
    8|      "id" : "1112269b3bf99403840e8934",  
    9|      "providerName" : "AWS",  
    10|      "provisioned" : true,  
    11|      "regionName" : "US_EAST_1",  
    12|      "vpcId" : "vpc-zz0zzzzz"  
    13|    } ],  
    14|    "totalCount":1  
    15| }  
  
What is MongoDB Atlas? →

