Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Clusters in All Projects

Share Feedback

On this page

  * Required Roles
  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Multi-Cloud Clusters Unsupported

Atlas excludes multi-cloud clusters from this endpoint's response.

Get details for all clusters in all projects available to the programmatic or
personal API key making the request.

## Required Roles

You can successfully call this endpoint with any assigned role.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /clusters  
      
  
### Request Path Parameters

This endpoint does not use HTTP request path parameters.

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
  
## Response

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

Name

|

Type

|

Description  
  
||  
  
clusters

|

array of objects

|

Objects that describe the clusters in each project that the API key is
authorized to view.  
  
clusters[n].alertCount

|

integer

|

Number of open alerts.  
  
clusters[n].authEnabled

|

boolean

|

Flag that indicates whether Atlas requires authenticationto access the nodes
in the cluster.

Atlas returns `true`.  
  
clusters[n].availability

|

string

|

Availability of the cluster. Values include:

  * `available`: All nodes in the cluster are available.

  * `warning`: Some nodes in the cluster are available. At least one node is unavailable.

  * `unavailable`: The cluster is unavailable. The cluster does not have a primary node.

  * `dead`: The cluster is inactive.

  
  
clusters[n].backupEnabled

|

boolean

|

Flag that indicates whether backup is enabled for the cluster.  
  
clusters[n].clusterId

|

string

|

Unique identifier of the Atlas cluster.  
  
clusters[n].dataSizeBytes

|

number

|

Total size of the data stored on each node in the cluster in bytes.  
  
clusters[n].name

|

string

|

Name of the cluster as it appears in Atlas.  
  
clusters[n].nodeCount

|

integer

|

Number of nodes in the cluster.  
  
clusters[n].sslEnabled

|

boolean

|

Flag that indicates whether SSL authentication is required to access the nodes
in the cluster.

Atlas returns `true`.  
  
clusters[n].type

|

string

|

Type of MongoDB cluster.

  * `replica set`: replica set

  * `sharded cluster`: sharded cluster

  
  
clusters[n].versions

|

array of strings

|

Version of MongoDB that each node in the cluster is running.  
  
groupId

|

string

|

Unique identifier of the project.  
  
groupName

|

string

|

Name of the project to which the returned clusters belong.  
  
orgId`

|

string

|

Unique identifier for the organization that owns the project to which the
returned clusters belong.  
  
orgName

|

string

|

Name of the organization that owns the project to which the returned clusters
belong.  
  
planType

|

string

|

Plan type.

Atlas returns `Atlas`.  
  
tags

|

array of strings

|

Tags applied to the project.

Atlas returns an empty array.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/clusters?pretty=true"  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    1| {  
    |  
    2|   "links": [  
    3|    {  
    4|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/clusters",  
    5|       "rel": "self"  
    6|     }  
    7|   ],  
    8|   "results": [  
    9|     {  
    10|       "clusters": [  
    11|         {  
    12|           "alertCount": 0,  
    13|           "authEnabled": true,  
    14|           "availability": "available",  
    15|           "backupEnabled": false,  
    16|           "clusterId": "5e6bc0352e41683c191c8956",  
    17|           "dataSizeBytes": 0,  
    18|           "name": "Cluster1",  
    19|           "nodeCount": 3,  
    20|           "sslEnabled": true,  
    21|           "type": "replica set",  
    22|           "versions": [  
    23|             "4.2.3"  
    24|           ]  
    25|         },  
    26|         {  
    27|           "alertCount": 0,  
    28|           "authEnabled": true,  
    29|           "availability": "available",  
    30|           "backupEnabled": false,  
    31|           "clusterId": "5e6bc60ba4c3f47a54d8fe95",  
    32|           "dataSizeBytes": 0,  
    33|           "name": "Cluster2",  
    34|           "nodeCount": 3,  
    35|           "sslEnabled": true,  
    36|           "type": "replica set",  
    37|           "versions": [  
    38|             "4.2.3"  
    39|           ]  
    40|         }  
    41|       ],  
    42|       "groupId": "5df90932f10fab675508b0e5",  
    43|       "groupName": "az",  
    44|       "orgId": "5df7a168f10fab3a149357fb",  
    45|       "orgName": "jww-12-16",  
    46|       "planType": "Atlas",  
    47|       "tags": []  
    48|     },  
    49|     {  
    50|       "clusters": [  
    51|         {  
    52|           "alertCount": 0,  
    53|           "authEnabled": true,  
    54|           "availability": "available",  
    55|           "backupEnabled": false,  
    56|           "clusterId": "5e6bbf6a9de0d35b1527dd93",  
    57|           "dataSizeBytes": 0,  
    58|           "name": "Cluster0",  
    59|           "nodeCount": 3,  
    60|           "sslEnabled": true,  
    61|           "type": "replica set",  
    62|           "versions": [  
    63|             "4.2.3"  
    64|           ]  
    65|         }  
    66|       ],  
    67|       "groupId": "5df90590f10fab5e33de2305",  
    68|       "groupName": "jww-12-17",  
    69|       "orgId": "5df7a168f10fab3a149357fb",  
    70|       "orgName": "jww-12-16",  
    71|       "planType": "Atlas",  
    72|       "tags": []  
    73|     },  
    74|     {  
    75|       "clusters": [  
    76|         {  
    77|           "alertCount": 0,  
    78|           "authEnabled": true,  
    79|           "availability": "dead",  
    80|           "backupEnabled": false,  
    81|           "clusterId": "5e6be93fd434591c4ca765f6",  
    82|           "dataSizeBytes": 0,  
    83|           "name": "Cluster0",  
    84|           "nodeCount": 0,  
    85|           "sslEnabled": true,  
    86|           "type": "replica set",  
    87|           "versions": [  
    88|             "4.2.3"  
    89|           ]  
    90|         }  
    91|       ],  
    92|       "groupId": "5df90923f10fab675508b065",  
    93|       "groupName": "gcp",  
    94|       "orgId": "5df7a168f10fab3a149357fb",  
    95|       "orgName": "jww-12-16",  
    96|       "planType": "Atlas",  
    97|       "tags": []  
    98|     }  
    99|   ],  
    100|   "totalCount": 3  
    101| }  
  
What is MongoDB Atlas? →

