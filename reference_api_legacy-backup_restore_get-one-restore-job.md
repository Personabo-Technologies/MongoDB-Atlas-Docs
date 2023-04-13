Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Legacy Backup Restore Job

Share Feedback

On this page

  * Syntax
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
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

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restoreJobs/{JOB-ID}  
      
  
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
  
`JOB-ID`

|

Required

|

Unique identifier for the restore job.  
  
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

This endpoint does not use HTTP request body parameters.

## Response Elements

The HTTP response returns a JSON document that includes the following
elements:

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
  
## Examples

### Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         -X GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/6b77777887d9d61443b41645/clusters/Cluster0/restoreJobs/6b77893b80eef5354c77ee15"  
  
### Example Response

    
    
    {  
      
      "batchId": "5a66783b80eef5354c77ee13",  
      "clusterId": "5a66689487d9d61443b46149",  
      "clusterName": "Cluster0",  
      "created": "2018-01-22T23:48:11Z",  
      "delivery": {  
        "expirationHours": 48,  
        "expires": "2018-01-22T23:49:38Z",  
        "maxDownloads": 2147483647,  
        "methodName": "HTTP",  
        "statusName": "EXPIRED",  
        "url": "https://api-backup.mongodb.com/backup/restore/v2/pull/6b77893b80eef5354c77ee15/N2Y1NDhkMjg0Mzk4NGU1Mzk3NTkwMjA0M2ZhODVkNDk=/Cluster0-shard-1-1516661094-6b77893b80eef5354c77ee15.tar.gz"  
      },  
      "encryptionEnabled": false,  
      "groupId": "5a66666887d9d61443b41645",  
      "hashes": [  
        {  
          "fileName": "Cluster0-shard-1-1516661094-6b77893b80eef5354c77ee15.tar.gz",  
          "hash": "86bc2f505c0874cdc0eaaa82ead2ef48aaf56d67",  
          "typeName": "SHA1"  
        }  
      ],  
      "id": "6b77893b80eef5354c77ee15",  
      "links": [  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5a66666887d9d61443b41645/clusters/Cluster0/restoreJobs/6b77893b80eef5354c77ee15",  
          "rel": "self"  
        },  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5a66666887d9d61443b41645/clusters/Cluster0",  
          "rel": "http://mms.mongodb.com/cluster"  
        },  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5a66666887d9d61443b41645/clusters/Cluster0/snapshots/5a6669d9fcc178211a0d86b9",  
          "rel": "http://mms.mongodb.com/snapshot"  
        },  
        {  
          "href": "https://cloud.mongodb.com/api/public/v1.0/groups/5a66666887d9d61443b41645",  
          "rel": "http://mms.mongodb.com/group"  
        }  
      ],  
      "pointInTime": false,  
      "snapshotId": "5a6669d9fcc178211a0d86b9",  
      "statusName": "FINISHED",  
      "timestamp": {  
        "date": "2018-01-22T22:44:54Z",  
        "increment": 1  
      }  
    }  
  
What is MongoDB Atlas? →

