Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Legacy Backup Restore Job

Share Feedback

On this page

  * Request
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Requests
  * Example Responses

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

Creates one restore job for the specified cluster.

This endpoint doesn't support the following:

  * Creating checkpoint restore jobs for sharded clusters

  * Creating restore jobs for queryable backup snapshots

## Important

If you create an automated restore job by specifying `delivery.methodName` of
`AUTOMATED_RESTORE` in your request body, Atlas **removes all existing data**
on the target cluster prior to the restore.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restoreJobs  
      
  
## Request Parameters

### Request Path Parameters

Path Parameter

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

Unique identifier of the project that owns the snapshots.  
  
`CLUSTER-NAME`

|

string

|

Required

|

Name of the cluster that contains the snapshots that you want to retrieve.  
  
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

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`checkpointId`

|

string

|

Conditional:

`"delivery.methodName" : "AUTOMATED_RESTORE"`

 _for Sharded Clusters Only._

|

Unique identifier for the sharded cluster checkpoint that represents the point
in time to which your data will be restored.

## Note

If you set `checkpointId`, you cannot set `oplogInc`, `oplogTs`, `snapshotId`,
or `pointInTimeUTCMillis`.

If you provide this setting, this endpoint restores all data up to this
checkpoint to the database you specify in the `delivery` object.  
  
`delivery`

|

object

|

Required

|

Method and details of how the restored snapshot data will be delivered.  
  
`delivery`

`.expirationHours`

|

number

|

Conditional:

`"delivery.methodName" : "HTTP"`

|

Number of hours the download URL is valid once the restore job is complete.  
  
`delivery`

`.maxDownloads`

|

number

|

Conditional:

`"delivery.methodName" : "HTTP"`

|

Number of times the download URL can be used. This must be `1` or greater.  
  
`delivery`

`.methodName`

|

string

|

Required

|

Means by which the data is delivered. Accepted values are:

  * `AUTOMATED_RESTORE`

  * `HTTP`

## Note

If you set `"delivery.methodName" : "AUTOMATED_RESTORE"`, you must also set:

  * `delivery.targetGroupId` and

  * `delivery.targetClusterName` or `delivery.targetClusterId`

In addition, the response shows the `delivery.methodName` as `HTTP`. An
automated restore uses the `HTTP` method to deliver the restore job to the
target host.  
  
`delivery`

`.targetClusterId`

|

string

|

Conditional:

`"delivery.methodName" : "AUTOMATED_RESTORE"`

|

Unique identifier of the target cluster. Use the `clusterId` returned in the
response body of the Get All Snapshots and Get a Snapshot endpoints. For use
only with automated restore jobs.

## Note

If backup is not enabled on the target cluster, the Get All Snapshots endpoint
returns an empty `results` array without `clusterId` elements, and the Get a
Snapshot endpoint also does not return a `clusterId` element. Use the
`delivery.targetClusterName` parameter instead or enable backup on the target
cluster.  
  
`delivery`

`.targetClusterName`

|

string

|

Conditional:

`"delivery.methodName" : "AUTOMATED_RESTORE"`

|

Name of the target cluster. Use the `clusterName` returned in the response
body of the Get All Snapshots and Get a Snapshot endpoints. For use only with
automated restore jobs.

## Note

If backup is not enabled on the target cluster, the Get All Snapshots endpoint
returns an empty `results` array without `clusterName` elements, and the Get a
Snapshot endpoint also does not return a `clusterName` element. Use the
`delivery.targetClusterName` parameter instead or enable backup on the target
cluster.  
  
`delivery`

`.targetGroupId`

|

string

|

Conditional:

`"delivery.methodName" : "AUTOMATED_RESTORE"`

|

Unique identifier of the project that contains the destination cluster for the
restore job.  
  
`oplogTs`

|

string

|

Conditional:

`"delivery.methodName" : "AUTOMATED_RESTORE"`

|

Oplog timestamp given as a timestamp in the number of seconds that have
elapsed since the UNIX epoch. When paired with `oplogInc`, they represent the
point in time to which your data will be restored.

Run a query against `local.oplog.rs` on your replica set to find the desired
timestamp.

## Note

If you set `oplogTs`, you:

  * Must set `oplogInc`.

  * Cannot set `checkpointId`, `snapshotId`, or `pointInTimeUTCMillis`.

If you provide this setting, this endpoint restores all data up to _and
including_ this Oplog timestamp to the database you specified in the
`delivery` object.  
  
`oplogInc`

|

string

|

Conditional:

`"delivery.methodName" : "AUTOMATED_RESTORE"`

|

32-bit incrementing ordinal that represents operations within a given second.
When paired with `oplogTs`, they represent the point in time to which your
data will be restored.

## Note

If you set `oplogInc`, you:

  * Must set `oplogTs`.

  * Cannot set `checkpointId`, `snapshotId`, or `pointInTimeUTCMillis`.

If you provide this setting, this endpoint restores all data up to _and
including_ this Oplog timestamp to the database you specified in the
`delivery` object.  
  
`pointInTimeUTCMillis`

|

long

|

Conditional:

`"delivery.methodName" : "AUTOMATED_RESTORE"`

|

timestamp in the number of milliseconds that have elapsed since the UNIX epoch
that represents the point in time to which your data will be restored. This
timestamp must be within last 24 hours of the current time.

If you provide this setting, this endpoint restores all data up to this point
in time to the database you specified in the `delivery` object.

## Note

If you set `pointInTimeUTCMillis`, you cannot set `oplogInc`, `oplogTs`,
`snapshotId`, or `checkpointId`.  
  
`snapshotId`

|

string

|

Required

|

Unique identifier of the snapshot to restore.

## Note

If you set `snapshotId`, you cannot set `oplogInc`, `oplogTs`,
`pointInTimeUTCMillis`, or `checkpointId`.  
  
## Response

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
  
## Example Requests

HTTP Restore

Automated Snapshot Restore

Automated Oplog Restore

Automated Continuous Cloud Backup

Automated Checkpoint Restore

Create a restore job that transfers a compressed snapshot using HTTP.

    
    
    curl --user "{USERNAME}:{APIKEY}" --digest \  
      
      --header "Accept: application/json" \  
      --header "Content-Type: application/json" \  
      --include \  
      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restoreJobs?pretty=true" \  
      --data '  
       {  
         "delivery" : {  
           "expirationHours" : "1",  
           "maxDownloads" : "1",  
           "methodName" : "HTTP"  
         },  
         "snapshotId" : "{SNAPSHOT-ID}"  
       }'  
  
## Example Responses

HTTP Restore

Automated Snapshot Restore

Automated Oplog Restore

Automated Continuous Cloud Backup

Automated Checkpoint Restore

    
    
    {  
      
      "batchId": "{BATCH-ID}",  
      "clusterId": "{CLUSTER-ID}",  
      "clusterName": "{CLUSTER-NAME}",  
      "created": "2018-09-20T15:00:00Z",  
      "delivery": {  
        "expirationHours": 1,  
        "maxDownloads": 1,  
        "methodName": "HTTP",  
        "statusName": "READY"  
      },  
      "encryptionEnabled": false,  
      "groupId": "{GROUP-ID}",  
      "id": "{RESTORE-JOB-ID}",  
      "links": [{  
        "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restoreJobs/{RESTORE-JOB-ID}",  
        "rel": "self"  
      }],  
      "pointInTime": false,  
      "snapshotId": "{SNAPSHOT-ID}",  
      "statusName": "FINISHED",  
      "timestamp": {  
        "date": "2018-09-15T15:53:00Z",  
        "increment": 1  
      }  
    }  
  
What is MongoDB Atlas? →

