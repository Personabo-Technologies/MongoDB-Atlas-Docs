Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Take One On-Demand Snapshot

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

Take one on-demand snapshot. Atlas takes on-demand snapshots immediately,
unlike scheduled snapshots which occur at regular intervals. If there is
already an on-demand snapshot with a status of **queued** or **inProgress** ,
you must wait until Atlas has completed the on-demand snapshot before taking
another.

## Required Roles

You must grant your API Key the `Project Owner` role to successfully call this
endpoint.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots  
      
  
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

Path Element

|

Type

|

Necessity

|

Description  
  
|||  
  
description

|

string

|

Required

|

Description of the on-demand snapshot.  
  
retentionInDays

|

number

|

Required

|

Number of days that Atlas should retain the on-demand snapshot. Must be at
least `1` .  
  
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

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
    |  
    2|      --digest --include \  
    3|      --header "Accept: application/json" \  
    4|      --header "Content-Type: application/json" \  
    5|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots?pretty=true" \  
    6|      --data '{  
    7|          "description": "On Demand Snapshot",  
    8|          "retentionInDays": 5  
    9|        }'  
  
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
    3|   "createdAt" : "2020-09-24T03:50:43Z",  
    4|   "description" : "On Demand Snapshot",  
    5|   "expiresAt" : "2020-09-29T03:50:43Z",  
    6|   "id" : "{SNAPSHOT-ID}",  
    7|   "links" : [ {  
    8|     "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots/{SNAPSHOT-ID}",  
    9|     "rel" : "self"  
    10|   }, {  
    11|     "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}",  
    12|     "rel" : "http://mms.mongodb.com/cluster"  
    13|   } ],  
    14|   "mongodVersion" : "4.0.20",  
    15|   "replicaSetName" : "newCluster",  
    16|   "snapshotType" : "onDemand",  
    17|   "status" : "queued",  
    18|   "storageSizeBytes" : 0,  
    19|   "type" : "replicaSet"  
    20| }  
  
What is MongoDB Atlas? →

