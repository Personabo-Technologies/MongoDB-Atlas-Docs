Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Cloud Backup

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request
  * Path Parameters
  * Query Parameters
  * Body Parameters
  * Response
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

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots/{SNAPSHOT-ID}  
      
  
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

Name of the Atlas cluster that contains the snapshot you want to retrieve.  
  
SNAPSHOT-ID

|

string

|

Required

|

Unique identifier of the snapshot you want to retrieve.  
  
### Query Parameters

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
  
### Body Parameters

This endpoint doesn't use HTTP request body parameters.

## Response

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
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots/{SNAPSHOT-ID}?pretty=true"  
  
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
    2|   "cloudProvider" : "AZURE",  
    3|   "createdAt": "2018-08-01T20:02:07Z",  
    4|   "expiresAt": "2018-08-04T20:03:11Z",  
    5|   "frequencyType": "hourly",  
    6|   "id": "{SNAPSHOT-ID}",  
    7|   "links": [  
    8|     {  
    9|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots/{SNAPSHOT-ID}",  
    10|       "rel": "self"  
    11|     },  
    12|     {  
    13|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}",  
    14|       "rel": "http://mms.mongodb.com/cluster"  
    15|     }  
    16|   ],  
    17|   "mongodVersion": "4.0.20",  
    18|   "policyItems": ['5e6244d0533d87725024d86e'],  
    19|   "replicaSetName" : "newCluster",  
    20|   "snapshotType" : "scheduled",  
    21|   "status" : "completed",  
    22|   "storageSizeBytes": 1778012160,  
    23|   "type" : "replicaSet"  
    24| }  
  
What is MongoDB Atlas? →

