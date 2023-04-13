Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Cloud Backup Restore Jobs

Share Feedback

On this page

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

Request \--=-

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs  
      
  
## Request Path Parameters

Parameter

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

Name of the Atlas cluster for which you want to retrieve restore jobs.  
  
## Request Query Parameters

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
  
## Request Body Parameters

This endpoint doesn't use HTTP request body parameters.

### Response

#### Response Document

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
  
#### results Embedded Document

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
  
### Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/MyCluster/backup/restoreJobs"  
  
### Example Response

    
    
    1| {  
    |  
    2|   "links": [],  
    3|   "results": [  
    4|     {  
    5|       "cancelled": false,  
    6|       "deliveryType": "automated",  
    7|       "expired": false,  
    8|       "expiresAt": "2020-08-02T02:08:48Z",  
    9|       "id": "{RESTORE-JOB-ID-1}",  
    10|       "links": [],  
    11|       "snapshotId": "{SNAPSHOT-ID}",  
    12|       "targetClusterName": "MyOtherCluster",  
    13|       "targetGroupId": "{GROUP-ID}",  
    14|       "timestamp": "2020-08-01T20:02:07Z"  
    15|     },  
    16|     {  
    17|       "cancelled": false,  
    18|       "createdAt": "2020-08-01T22:05:41Z",  
    19|       "deliveryType": "download",  
    20|       "deliveryUrl": "https://restore.example.com:27017/restore-{RESTORE-JOB-ID-2}.tar.gz",  
    21|       "expired": false,  
    22|       "expiresAt": "2020-08-02T02:03:33Z",  
    23|       "id": "{RESTORE-JOB-ID-2}",  
    24|       "links": [],  
    25|       "snapshotId": "{SNAPSHOT-ID}",  
    26|       "timestamp": "2020-08-01T20:02:07Z"  
    27|     }  
    28|   ],  
    29|   "totalCount": 2  
    30| }  
  
What is MongoDB Atlas? →

