Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Network Peering Containers in One Project

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

Retrieve a list of Network Peering containers in one project. You must have
the `Project Read Only` or a more permissive role to successfully call this
endpoint.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/containers/all  
      
  
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

This endpoint may use any of the HTTP request query parameters available to
all Atlas Administration API resources. These are all optional.

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

Response Element

|

Type

|

Description

|

Provider  
  
|||  
  
`atlasCidrBlock`

|

string

|

CIDR block that Atlas uses for your clusters.

|

AWS, Azure, GCP  
  
`azureSubscriptionId`

|

string

|

Unique identifer of the Azure subscription in which the VNet resides.

|

Azure  
  
`gcpProjectId`

|

string

|

Unique identifier of the Google Cloud project in which the network peer
resides. Returns `null` until a peering connection is created. Maps to the
Atlas GCP Project ID field returned when you create a VPC in the Atlas
console.

You must provide this value when you create a VPC in Google Cloud.

|

GCP  
  
`id`

|

string

|

Unique identifier of the Network Peering container.

|

AWS, Azure, GCP  
  
`networkName`

|

string

|

Unique identifier of the Network Peering connection in the Atlas project.
Returns `null` until a peering connection is created. Maps to the Atlas VPC
Name field returned when you create a VPC in the Atlas console.

You must provide this value when you create a VPC in Google Cloud.

|

GCP  
  
`providerName`

|

string

|

Cloud provider for this Network Peering connection.

|

AWS, Azure, GCP  
  
`provisioned`

|

boolean

|

Flag that indicates if the project has clusters deployed in the Network
Peering container or Azure VNet.

|

AWS, Azure, GCP  
  
`region`

|

string

|

AWS region where the VCP resides or Azure region where the VNet resides.

|

AWS, Azure  
  
`vnetName`

|

string

|

Unique identifier of your Azure VNet. The value is `null` if there are no
network peering connections in the container.

|

Azure  
  
`vpcId`

|

string

|

Unique identifier of the project's Network Peering container.

|

AWS  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/containers/all?pretty=true"  
  
## Example Response

    
    
    1| {  
    |  
    2|   "links":[ {  
    3|      "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/containers?pageNum=1&itemsPerPage=100",  
    4|      "rel" : "self"  
    5|   } ],  
    6|   "results":[ {  
    7|     "atlasCidrBlock" : "10.8.0.0/21",  
    8|     "id" : "1112269b3bf99403840e8934",  
    9|     "providerName" : "AWS",  
    10|     "provisioned" : true,  
    11|     "regionName" : "US_EAST_1",  
    12|     "vpcId" : "vpc-zz0zzzzz"  
    13|   }, {  
    14|     "atlasCidrBlock" : "10.8.0.0/18",  
    15|     "id" : "1112269b3bf99403840e8934",  
    16|     "gcpProjectId" : "my-sample-project-191923",  
    17|     "networkName" : "test1",  
    18|     "providerName" : "GCP",  
    19|     "provisioned" : true  
    20|   }, {  
    21|     "atlasCidrBlock" : "192.168.248.0/21",  
    22|     "azureSubscriptionId" : "602336d43d098d433845971g",  
    23|     "id" : "5cb5f17280eef56a459fa2ea",  
    24|     "providerName" : "AZURE",  
    25|     "provisioned" : true,  
    26|     "region" : "US_EAST_2",  
    27|     "vnetName" : "vnet_6dc5f17280eef56a459fa2ea_cucjobcas"  
    28|   } ],  
    29|   "totalCount" : 3  
    30| }  
  
What is MongoDB Atlas? →

