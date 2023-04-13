Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Cloud Backup Restore Job

Share Feedback

On this page

  * Request
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

## Important

If you specify `"deliveryType" : "automated"` or `"deliveryType" :
"pointInTime"` in your request body to create an automated restore job, Atlas
**removes all existing data** on the target cluster prior to the restore.

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

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs/  
      
  
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

Unique identifier of the project for the Atlas cluster whose snapshot you want
to restore.  
  
SOURCE-CLUSTER-NAME

|

string

|

Required

|

Name of the Atlas cluster whose snapshot you want to restore.  
  
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
  
The request body, response body, and examples depend on the type of restore:

Automated

Continuous Cloud Backup

Downloaded

### Request Body Parameters

Automated

Continuous Cloud Backup

Downloaded

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
deliveryType

|

string

|

Required

|

Type of restore job to create. Accepted values include:

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
  
snapshotId

|

string

|

Required

|

Unique identifier of the snapshot to restore.  
  
target

ClusterName

|

string

|

Required

|

Name of the target Atlas cluster to which the restore job restores the
snapshot.  
  
target

GroupId

|

string

|

Required

|

Unique identifier of the target Atlas project for the specified
**targetClusterName**.  
  
## Response

Automated

Continuous Cloud Backup

Downloaded

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
restore job.  
  
deliveryType

|

string

|

Type of restore job to create. Atlas may return:

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
  
snapshotId

|

string

|

Unique identifier of the source snapshot ID of the restore job.  
  
targetGroupId

|

string

|

Name of the target Atlas project of the restore job.  
  
targetClusterName

|

string

|

Name of the target Atlas cluster to which the restore job restores the
snapshot.  
  
timestamp

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the snapshot associated
to **snapshotId** was taken.  
  
## Example Request

Automated

Continuous Cloud Backup

Downloaded

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{SOURCE-CLUSTER-NAME}/backup/restoreJobs" \  
    5|      --data '{  
    6|          "snapshotId" : "{SNAPSHOT-ID}",  
    7|          "deliveryType" : "automated",  
    8|          "targetClusterName" : "{TARGET-CLUSTER-NAME}",  
    9|          "targetGroupId" : "{TARGET-GROUP-ID}"  
    10|        }'  
  
## Example Response

Automated

Continuous Cloud Backup

Downloaded

    
    
    1| {  
    |  
    2|   "cancelled": false,  
    3|   "deliveryType": "automated",  
    4|   "expired": false,  
    5|   "expiresAt": "2020-05-04T16:25:01Z",  
    6|   "id": "{RESTORE-ID}",  
    7|   "links": [  
    8|     {  
    9|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{SOURCE-CLUSTER-NAME}/backup/restoreJobs/{RESTORE-ID}",  
    10|       "rel": "self"  
    11|     },  
    12|     {  
    13|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{SOURCE-CLUSTER-NAME}/backup/snapshots/{SNAPSHOT-ID}",  
    14|       "rel": "http://mms.mongodb.com/snapshot"  
    15|     },  
    16|     {  
    17|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{SOURCE-CLUSTER-NAME}",  
    18|       "rel": "http://mms.mongodb.com/cluster"  
    19|     },  
    20|     {  
    21|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}",  
    22|       "rel": "http://mms.mongodb.com/group"  
    23|     }  
    24|   ],  
    25|   "snapshotId": "{SNAPSHOT-ID}",  
    26|   "targetClusterName": "{TARGET-CLUSTER-NAME}",  
    27|   "targetGroupId": "{TARGET-GROUP-ID}",  
    28|   "timestamp": "2020-05-03T16:25:01Z"  
    29| }  
  
What is MongoDB Atlas? →

