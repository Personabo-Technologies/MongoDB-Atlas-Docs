Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Cloud Backups

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request
  * Path Parameters
  * Query Parameters
  * Body Parameters
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

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You must grant your API Key the `Project Read Only` role to successfully call
this endpoint.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots  
      
  
## Request

### Path Parameters

Path Element

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

Unique identifier of the project for the Atlas cluster.  
  
CLUSTER-NAME

|

string

|

Required

|

Name of the Atlas cluster that contains the snapshots you want to retrieve.  
  
### Query Parameters

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
  
### Body Parameters

This endpoint doesn't use HTTP request body parameters.

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
  
cloudProvider

|

string

|

Cloud provider that stores this snapshot. Atlas returns this parameter when
**"type": "replicaSet"**.  
  
createdAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas took the
snapshot. Atlas sorts the `results` document in descending order based on this
date.  
  
description

|

string

|

Description of the snapshot. Atlas returns this parameter when **"status":
"onDemand"**.  
  
expiresAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas deletes the
snapshot.  
  
frequencyType

|

string

|

Human-readable label that indicates the rate at which the backup policy item
occurs. Value can be one of the following: `ondemand`, `hourly`, `daily`,
`weekly`, or `monthly`.  
  
id

|

string

|

Unique identifier of the snapshot.  
  
links

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
masterKeyUUID

|

string

|

Unique identifier of the AWS KMS Customer Master Key used to encrypt the
snapshot. Atlas returns this value for clusters using Encryption at Rest via
Customer KMS.  
  
members

|

array of objects

|

List of snapshots and the cloud provider where the snapshots are stored. Atlas
returns this parameter when **"type": "shardedCluster"**.  
  
members[n]

.cloudProvider

|

string

|

Cloud provider that stores this snapshot.  
  
members[n].id

|

string

|

Unique identifier for the sharded cluster snapshot.  
  
members[n].replicaSetName

|

string

|

Label given to a shard or config server from which Atlas took this snapshot.  
  
mongodVersion

|

string

|

Version of the MongoDB server.  
  
policyItems

|

array of strings

|

List that contains unique identifiers for each backup policy item.  
  
replicaSetName

|

string

|

Label given to the replica set from which Atlas took this snapshot. Atlas
returns this parameter when **"type": "replicaSet"**.  
  
snapshotIds

|

array of strings

|

Unique identifiers of the snapshots created for the shards and config server
for a sharded cluster. Atlas returns this parameter when **"type":
"shardedCluster"**. These identifiers should match those given in the
**members[n].id** parameters. This allows you to map a snapshot to its shard
or config server name.  
  
snapshotType

|

string

|

Type of snapshot. Atlas can return **onDemand** or **scheduled**.  
  
status

|

string

|

Current status of the snapshot. Atlas can return one of the following values:

  *  **queued**

  *  **inProgress**

  *  **completed**

  *  **failed**

  
  
storageSizeBytes

|

integer

|

Size of the snapshot in bytes.  
  
type

|

string

|

Type of cluster. Atlas can return **replicaSet** or **shardedCluster**.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots?pretty=true"  
  
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

Replica Set

Sharded Clusters

    
    
    1| {  
    |  
    2|   "links": [  
    3|     {  
    4|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots?pageNum=1&itemsPerPage=100",  
    5|       "rel": "self"  
    6|     }  
    7|   ],  
    8|   "results": [  
    9|     {  
    10|       "cloudProvider" : "AZURE",  
    11|       "createdAt": "2018-08-01T20:02:07Z",  
    12|       "expiresAt": "2018-08-04T20:03:11Z",  
    13|       "frequencyType": "hourly",  
    14|       "id": "{SNAPSHOT-ID}",  
    15|       "links": [  
    16|         {  
    17|           "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots/{SNAPSHOT-ID}",  
    18|           "rel": "self"  
    19|         },  
    20|         {  
    21|           "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}",  
    22|           "rel": "http://mms.mongodb.com/cluster"  
    23|         }  
    24|       ],  
    25|       "mongodVersion": "4.0.20",  
    26|       "policyItems": ['5e6244d0533d87725024d86e'],  
    27|       "replicaSetName" : "newCluster",  
    28|       "snapshotType" : "scheduled",  
    29|       "status" : "completed",  
    30|       "storageSizeBytes": 1778012160,  
    31|       "type" : "replicaSet"  
    32|     }  
    33|   ],  
    34|   "totalCount": 1  
    35| }  
  
What is MongoDB Atlas? →

