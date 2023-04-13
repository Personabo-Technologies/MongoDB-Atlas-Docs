Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Legacy Backup Restore Jobs

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

Get all restore jobs for a cluster. `CLUSTER-NAME` must be the name of either
a replica set or a sharded cluster.

## Note

If you use the `BATCH-ID` query parameter, you can retrieve all restore jobs
in the specified batch. When creating a restore job for a sharded cluster,
Atlas creates a separate job for each shard, plus another for the config
server. Each of those jobs are part of a batch. A restore job for a replica
set, however, cannot be part of a batch.

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

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restoreJobs  
      
      
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restoreJobs?batchId={BATCH-ID}  
      
  
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

Required

|

Unique identifier of the project that owns the snapshots.  
  
`CLUSTER-NAME`

|

Required

|

Name of the cluster that contains the snapshots that you want to retrieve.  
  
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
  
|

|

|

|  
  
||||  
  
batchId

|

string

|

Optional

|

Unique identifier of the batch.

|  
  
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
  
`batchId`

|

string

|

Unique identifier of the batch to which this restore job belongs.

Only present for a restore of a sharded cluster.  
  
`clusterId`

|

string

|

Unique identifier of the cluster the restore job represents.

Only present for a restore of a cluster.  
  
`created`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the restore job was
requested.  
  
`delivery`

|

object

|

Method and details of how the restored snapshot data shall be delivered.  
  
`delivery.expires`

|

string

|

Timestamp in ISO 8601 date and time format in UTC after which the URL is no
longer available.

Only present if `"delivery.methodName" : "HTTP"`.  
  
`delivery.expirationHours`

|

number

|

Number of hours the download URL is valid once the restore job is complete.

Only present if `"delivery.methodName" : "HTTP"`.  
  
`delivery.maxDownloads`

|

number

|

Number of times the download URL can be used. This must be `1` or greater.

Only present if `"delivery.methodName" : "HTTP"`.  
  
`delivery.methodName`

|

string

|

Means by which the data is delivered. Accepted values include:

  * `HTTP`

  * `QUERY`

  
  
`delivery.statusName`

|

string

|

Current status of the downloadable file. Accepted values include:

  * `NOT_STARTED`

  * `IN_PROGRESS`

  * `READY`

  * `FAILED`

  * `INTERRUPTED`

  * `EXPIRED`

  * `MAX_DOWNLOADS_EXCEEDED`

  
  
`delivery.url`

|

string

|

URL from which the restored snapshot data can be downloaded.

Only present if `"delivery.methodName" : "HTTP"`.  
  
`encryptionEnabled`

|

boolean

|

Indicates whether the restored snapshot data is encrypted.  
  
`groupId`

|

string

|

Unique identifier of the project that owns the restore job.  
  
`hashes`

|

object array

|

If the corresponding `delivery.url` has been downloaded, each document in this
array is a mapping of a restore file to a hashed checksum. This array is
present _only after_ the file is downloaded.

## Note

For an `HTTP` restore, this array only contains a single object that
represents the hash of the `.tar.gz` file.  
  
`hashes.typeName`

|

string

|

Hashing algorithm used to compute the hash value. If present, this value is
`SHA1`.  
  
`hashes.fileName`

|

string

|

Name of the file that has been hashed.  
  
`hashes.hash`

|

string

|

Hash of the file.  
  
`id`

|

string

|

Unique identifier of the restore job.  
  
`links`

|

document array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
`masterKeyUUID`

|

string

|

KMIP master key ID used to encrypt the snapshot data.

Only if `encryptionEnabled` is true for the snapshot.  
  
`snapshotId`

|

string

|

Unique identifier of the snapshot to restore.  
  
`statusName`

|

string

|

Current status of the job. Accepted values include:

  * `FINISHED`

  * `IN_PROGRESS`

  * `BROKEN`

  * `KILLED`

  
  
`timestamp`

|

object

|

Timestamp of the Oplog entry when the snapshot was created.  
  
`timestamp.date`

|

string

|

Timestamp in ISO 8601 date and time format in UTC of the latest oplog entry in
the restored snapshot.  
  
`timestamp.increment`

|

string

|

Order of all operations completed at the latest oplog entry in the restored
snapshot.  
  
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

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         -X GET  "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-ID}/restoreJobs"  
  
### Example Response

    
    
    {  
      
      "links": [  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/6b77777887d9d61443b41645/clusters/Cluster0/restoreJobs?pageNum=1&itemsPerPage=100",  
          "rel": "self"  
        }  
      ],  
      "results": [  
        {  
          "batchId": "5a66783b80eef5354c77ee13",  
          "clusterId": "7c88887880eef52e5f4d0e2d",  
          "clusterName": "Cluster0",  
          "created": "2018-01-22T23:48:11Z",  
          "delivery": {  
            "expirationHours": 48,  
            "expires": "2018-01-22T23:49:38Z",  
            "maxDownloads": 2147483647,  
            "methodName": "HTTP",  
            "statusName": "EXPIRED",  
            "url": "https://api-backup.mongodb.com/backup/restore/v2/pull/5a66783b80eef5354c77ee16/MGViYTUwZGQ4YWVkNDY4MGE2YWE4NGQzODY0MzAzYTU=/config-Cluster0-config-0-5a66689487d9d61443b46149-1516661094-5a66783b80eef5354c77ee16.tar.gz"  
          },  
          "encryptionEnabled": false,  
          "groupId": "6b77777887d9d61443b41645",  
          "hashes": [  
            {  
              "fileName": "config-Cluster0-config-0-5a66689487d9d61443b46149-1516661094-5a66783b80eef5354c77ee16.tar.gz",  
              "hash": "a98af3c1f85a9eb3061423cda0fad8b4d0a48209",  
              "typeName": "SHA1"  
            }  
          ],  
          "id": "5a66783b80eef5354c77ee16",  
          "links": [  
            {  
              "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/6b77777887d9d61443b41645/clusters/Cluster0/restoreJobs/5a66783b80eef5354c77ee16",  
              "rel": "self"  
            }  
          ],  
          "pointInTime": false,  
          "snapshotId": "5a6669d5e2bfb3461861360c",  
          "statusName": "FINISHED",  
          "timestamp": {  
            "date": "2018-01-22T22:44:54Z",  
            "increment": 1  
          }  
        },  
        {  
          "batchId": "5a66783b80eef5354c77ee13",  
          "clusterId": "6b88887880eef52e5f4d0e2f",  
          "clusterName": "Cluster0",  
          "created": "2018-01-22T23:48:11Z",  
          "delivery": {  
            "expirationHours": 48,  
            "expires": "2018-01-22T23:49:38Z",  
            "maxDownloads": 2147483647,  
            "methodName": "HTTP",  
            "statusName": "EXPIRED",  
            "url": "https://api-backup.mongodb.com/backup/restore/v2/pull/5a66783b80eef5354c77ee15/N2Y1NDhkMjg0Mzk4NGU1Mzk3NTkwMjA0M2ZhODVkNDk=/Cluster0-shard-1-1516661094-5a66783b80eef5354c77ee15.tar.gz"  
          },  
          "encryptionEnabled": false,  
          "groupId": "6b77777887d9d61443b41645",  
          "hashes": [  
            {  
              "fileName": "Cluster0-shard-1-1516661094-5a66783b80eef5354c77ee15.tar.gz",  
              "hash": "86bc2f505c0874cdc0eaaa82ead2ef48aaf56d67",  
              "typeName": "SHA1"  
            }  
          ],  
          "id": "5a66783b80eef5354c77ee15",  
          "links": [  
            {  
              "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/6b77777887d9d61443b41645/clusters/Cluster0/restoreJobs/5a66783b80eef5354c77ee15",  
              "rel": "self"  
            }  
          ],  
          "pointInTime": false,  
          "snapshotId": "5a6669d9fcc178211a0d75a8",  
          "statusName": "FINISHED",  
          "timestamp": {  
            "date": "2018-01-22T22:44:54Z",  
            "increment": 1  
          }  
        },  
        {  
          "batchId": "5a66783b80eef5354c77ee13",  
          "clusterId": "6b99987880eef52e5f4d0e31",  
          "clusterName": "Cluster0",  
          "created": "2018-01-22T23:48:11Z",  
          "delivery": {  
            "expirationHours": 48,  
            "expires": "2018-01-22T23:49:38Z",  
            "maxDownloads": 2147483647,  
            "methodName": "HTTP",  
            "statusName": "EXPIRED",  
            "url": "https://api-backup.mongodb.com/backup/restore/v2/pull/5a66783b80eef5354c77ee14/NjMxOWFhNTA3MGY1NDU0Mzk5ZDU1YjE0YWY2ZjQ5NDM=/Cluster0-shard-0-1516661094-5a66783b80eef5354c77ee14.tar.gz"  
          },  
          "encryptionEnabled": false,  
          "groupId": "6b77777887d9d61443b41645",  
          "hashes": [  
            {  
              "fileName": "Cluster0-shard-0-1516661094-5a66783b80eef5354c77ee14.tar.gz",  
              "hash": "18a8617d0b6bfff97b7232d1ebeeea16edc216b0",  
              "typeName": "SHA1"  
            }  
          ],  
          "id": "5a66783b80eef5354c77ee14",  
          "links": [  
            {  
              "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/6b77777887d9d61443b41645/clusters/Cluster0/restoreJobs/5a66783b80eef5354c77ee14",  
              "rel": "self"  
            }  
          ],  
          "pointInTime": false,  
          "snapshotId": "5a6669d9e2bfb34668cfe459",  
          "statusName": "FINISHED",  
          "timestamp": {  
            "date": "2018-01-22T22:44:54Z",  
            "increment": 1  
          }  
        }  
      ],  
      "totalCount": 3  
    }  
  
What is MongoDB Atlas? →

