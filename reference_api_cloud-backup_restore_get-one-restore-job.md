Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Cloud Backup Restore Job

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response

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

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs/{RESTORE-JOB-ID}  
      
  
### Request Path Parameters

Path Parameter

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

Name of the Atlas cluster from which you want to retrieve the restore job.  
  
RESTORE-JOB-ID

|

string

|

Required

|

Unique identifier of the restore job to retrieve.  
  
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

This endpoint doesn't use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
cancelled

|

boolean

|

Flag indicating whether the restore job was canceled.  
  
createdAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas created the
restore job. Atlas sorts the `results` document in descending order based on
this date.  
  
components

|

array of objects

|

Collection of clusters to be downloaded. Atlas returns this parameter when
restoring a sharded cluster and **"deliveryType" : "download"**.  
  
components

.downloadUrl

|

string

|

URL from which the snapshot of the **components.replicaSetName** should be
downloaded. Atlas returns **null** for this parameter if the download URL:

  * Has expired,

  * Has been used, or

  * Hasn't been created.

  
  
components

.replicaSetName

|

string

|

Name of the shard or config server included in the snapshot.  
  
deliveryType

|

string

|

Type of restore job to create. Possible values are:

|

Job Type

|

Action  
  
|  
  
automated

|

Atlas restores the snapshot corresponding to the **snapshotId** to the Atlas
cluster corresponding to the name **targetClusterName** in the Atlas project
corresponding to the **targetGroupId**.  
  
download

|

Atlas generates and displays a URL to download a `.tar.gz` of the snapshot
corresponding to the **snapshotId**. The contents of the **tar.gz** archive
contain the data files for your Atlas cluster.

## Tip

### See also:

To learn more about manually restoring the downloaded data files, see
Procedure.

## Note

### Download Limitations

Each cloud backup can have one download at a time, and each project can have a
maximum of 20 downloads at a time.  
  
pointInTime

|

Atlas performs a Continuous Cloud Backup restore.  
  
deliveryUrl

|

array of strings

|

One or more URLs for the compressed snapshot files for manual download. Atlas
returns this parameter when **"deliveryType" : "download"**.

## Note

If empty, Atlas is processing the restore job. Use the Get All Cloud Backup
Restore Jobs endpoint periodically check for a **deliveryUrl** download value
for the restore job.  
  
expired

|

boolean

|

Flag indicating whether the restore job expired.  
  
expiresAt

|

integer

|

Timestamp in ISO 8601 date and time format in UTC when the restore job
expires.  
  
failed

|

boolean

|

Flag indicating whether the restore job failed.  
  
finishedAt

|

integer

|

Timestamp in ISO 8601 date and time format in UTC when the restore job
completed.  
  
id

|

string

|

Unique identifier of the restore job.  
  
links

|

array of objects

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
oplogTs

|

integer

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch from
which to you want to restore this snapshot. This is the first part of an Oplog
timestamp. Atlas returns this parameter when **"deliveryType" :
"pointInTime"** and **"oplogTs" > 0**.

## Note

Serverless instance snapshots don't return the `oplogTs`. You can't restore a
serverless instance snapshot using an Oplog timestamp.  
  
oplogInc

|

integer

|

Oplog operation number from which to you want to restore this snapshot. This
is the second part of an Oplog timestamp. Atlas returns this parameter when
**"deliveryType" : "pointInTime"** and **"oplogTs" > 0**.

## Note

Serverless instance snapshots don't return the `oplogInc`. You can't restore a
serverless instance snapshot using an Oplog timestamp.  
  
pointInTimeUTCSeconds

|

integer

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch from
which Atlas restored this snapshot. Returned when **"deliveryType" :
"pointInTime"** and **"pointInTimeUTCSeconds" > 0**.  
  
snapshotId

|

string

|

Unique identifier of the source snapshot ID of the restore job. Returned when
**"deliveryType" : "automated"** or **"deliveryType" : "download"**.  
  
targetGroupId

|

string

|

Name of the target Atlas project of the restore job. Returned when
**"deliveryType" : "automated"**.  
  
targetClusterName

|

string

|

Name of the target Atlas cluster to which the restore job restores the
snapshot. Atlas returns this parameter when **"deliveryType" : "automated"**.  
  
timestamp

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the snapshot associated
to **snapshotId** was taken.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs/{RESTORE-JOB-ID}"  
  
## Example Response

    
    
    1| {  
    |  
    2|   "cancelled": false,  
    3|   "deliveryType": "automated",  
    4|   "expired": false,  
    5|   "expiresAt": "2018-08-02T02:08:48Z",  
    6|   "failed" : false,  
    7|   "id": "{RESTORE-JOB-ID}",  
    8|   "links": [  
    9|     {  
    10|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs/{RESTORE-JOB-ID}",  
    11|       "rel": "self"  
    12|     },  
    13|     {  
    14|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots/{SNAPSHOT-ID}",  
    15|       "rel": "http://mms.mongodb.com/snapshot"  
    16|     },  
    17|     {  
    18|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}",  
    19|       "rel": "http://mms.mongodb.com/cluster"  
    20|     },  
    21|     {  
    22|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}",  
    23|       "rel": "http://mms.mongodb.com/group"  
    24|     }  
    25|   ],  
    26|   "snapshotId": "{SNAPSHOT-ID}",  
    27|   "targetClusterName": "MyOtherCluster",  
    28|   "targetGroupId": "{GROUP-ID}",  
    29|   "timestamp": "2018-08-01T20:02:07Z"  
    30| }  
  
What is MongoDB Atlas? →

