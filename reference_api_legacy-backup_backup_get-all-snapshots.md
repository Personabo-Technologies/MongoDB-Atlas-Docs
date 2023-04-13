Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Snapshots

Share Feedback

On this page

  * Syntax
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * `results` Array
  * `links` Array
  * `totalCount` Document
  * Examples
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Legacy Backup Deprecated

Effective 23 March 2020, all new clusters can _only_ use Cloud Backups.

When you upgrade to 4.2, your backup system upgrades to cloud backup if it is
currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/snapshots  
      
  
## Request Parameters

### Request Path Parameters

Path Element

|

Necessity

|

Description  
  
||  
  
`GROUP-ID`

|

Required.

|

The unique identifier of the project that owns the snapshots.  
  
`CLUSTER-NAME`

|

Required

|

The name of the cluster that contains the snapshots that you want to retrieve.  
  
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

This endpoint does not use HTTP request body parameters.

## Response Elements

The HTTP response returns a JSON document that includes the following
elements:

### `results` Array

Name

|

Type

|

Description  
  
||  
  
`clusterId`

|

string

|

The unique ID of the cluster that the snapshot represents.  
  
`complete`

|

boolean

|

Indicates whether the snapshot exists. This is `false` if the snapshot
creation job is in progress.  
  
`created`

|

Document

|

The components of a timestamp.  
  
`created.date`

|

timestamp

|

The exact point in time when the snapshot was taken in ISO 8601 date and time
format in UTC.  
  
`created.increment`

|

integer

|

The operation order in which this snapshot took place at this exact point in
time. To learn how timestamps work in MongoDB, see timestamp.  
  
`doNotDelete`

|

boolean

|

Specifies whether the snapshot can be deleted.  
  
`expires`

|

timestamp

|

The date in ISO 8601 date and time format in UTC after which Atlas deletes the
snapshot.

If `doNotDelete` is set to `true`, any value in `expires` is removed.

If the `expires` value is earlier than the current date and time, the snaphot
cannot be edited.  
  
`groupId`

|

objectId

|

ID of the project that owns the snapshot.  
  
`id`

|

objectId

|

ID of the snapshot.  
  
`lastOplogAppliedTimestamp`

|

document

|

The components of the timestamp of the last oplog entry was applied.  
  
`lastOplogAppliedTimestamp.date`

|

timestamp

|

The exact point in time when the last oplog was applied in ISO 8601 date and
time format in UTC.  
  
`lastOplogAppliedTimestamp.increment`

|

integer

|

The operation order in which the last oplog was applied at this exact point in
time. To learn how timestamps work in MongoDB, see timestamp.  
  
`links`

|

document array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification.  
  
`parts`

|

document array

|

The individual parts that comprise the complete snapshot.

  * For a replica set, this array contains a single document.

  * For a sharded cluster, this array contains one document for each shard plus one document for the config server.

  
  
`parts.clusterId`

|

objectId

|

ID of the replica set.  
  
`parts.compressionSetting`

|

string

|

Method of compression for the snapshot.  
  
`parts.dataSizeBytes`

|

number

|

The total size of the data in the snapshot in bytes.  
  
`parts.encryptionEnabled`

|

boolean

|

Indicates whether the snapshot is encrypted.  
  
`parts.fileSizeBytes`

|

number

|

The total size of the data files in bytes.  
  
`parts.masterKeyUUID`

|

objectId

|

The KMIP master key ID used to encrypt the snapshot data.

## Note

### This appears only if parts.encryptionEnabled is true.  
  
`parts.mongodVersion`

|

string

|

The version of MongoDB that the replica set primary was running when the
snapshot was created.  
  
`parts.replicaSetName`

|

string

|

Name of the replica set.  
  
`parts.storageSizeBytes`

|

number

|

The total size of space allocated for document storage.  
  
`parts.typeName`

|

string

|

The type of server that the part represents:

  * `REPLICA_SET`

  * `CONFIG_SERVER_REPLICA_SET`

  
  
### `links` Array

The `links` array includes one or more links to sub-resources and/or related
resources. The relations between URLs are explained in the Web Linking
Specification.

Relation

|

Description  
  
|  
  
`self`

|

The URL endpoint for this resource.  
  
### `totalCount` Document

This value is the count of the total number of items in the result set.
`totalCount` may be greater than the number of objects in the `results` array
if the entire result set is paginated.

## Examples

### Example Request

    
    
    curl -X GET -i --digest -u "{PUBLIC-KEY}:{PRIVATE-KEY}" "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/snapshots"  
      
  
### Example Response

    
    
    HTTP/1.1 200 OK  
      
      
    {  
    "links": [{  
       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/snapshots?pageNum=1&itemsPerPage=100",  
       "rel": "self"  
    }],  
    "results": [{  
       "clusterId": "{CLUSTER-ID}",  
       "complete": true,  
       "created": {  
          "date": "2017-12-26T16:32:16Z",  
          "increment": 1  
       },  
       "doNotDelete": false,  
       "expires": "2018-12-25T16:32:16Z",  
       "groupId": "{GROUP-ID}",  
       "id": "{SNAPSHOT-ID}",  
       "lastOplogAppliedTimestamp": {  
          "date": "2017-12-26T16:32:15Z",  
          "increment": 1  
       },  
       "links": [{  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/6c7498dg87d9e6526801572b/clusters/Cluster0/snapshots/5a4279d4fcc178500596745a",  
          "rel": "self"  
       }],  
       "parts": [{  
          "clusterId": "{CLUSTER-ID}",  
          "compressionSetting": "GZIP",  
          "dataSizeBytes": 4502,  
          "encryptionEnabled": false,  
          "fileSizeBytes": 324760,  
          "mongodVersion": "4.0.0",  
          "replicaSetName": "Cluster0-shard-0",  
          "storageSizeBytes": 53248,  
          "typeName": "REPLICA_SET"  
       }]  
    }],  
    "totalCount": 1  
    }  
  
What is MongoDB Atlas? →

