Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Cloud Backup Snapshot Export Job

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

The `/backup/exports` resource enables you to export one backup snapshot for
an `M10` or higher Atlas cluster with Back Up Your Database Deployment enabled
to an AWS bucket.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/exports/  
      
  
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

Unique 24-hexadecimal digit string that identifies the project which contains
the Atlas cluster whose snapshot you want to export.  
  
CLUSTER-NAME

|

string

|

Required

|

Name of the Atlas cluster whose snapshot you want to export.  
  
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

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
snapshotId

|

string

|

Required

|

Unique identifier of the Cloud Backup snasphot to export. If necessary, use
the Get All Cloud Backups API to retrieve the list of snapshot IDs for a
cluster.  
  
exportBucketId

|

string

|

Required

|

Unique identifier of the AWS bucket to export the Cloud Backup snasphot to. If
necessary, use the Get All Snapshot Export Buckets API to retrieve the IDs of
all available export buckets for a project.  
  
customData

|

array of documents

|

Optional

|

Custom data to include in the metadata file named `.complete` that Atlas
uploads to the bucket when the export job finishes. Custom data can be
specified as key and value pairs.  
  
customData.key

|

string

|

Required

|

Required if you want to include custom data using `customData` in the metadata
file uploaded to the bucket.

Key to include in the metadata file that Atlas uploads to the bucket when the
export job finishes.  
  
customData.value

|

string

|

Required

|

Required if you specify `customData.key`.

Value for the key specified using `customData.key`.  
  
## Response

Name

|

Type

|

Description  
  
||  
  
`components`

|

array of documents

|

 _Returned for sharded clusters only._

Export job details for each replica set in the sharded cluster.  
  
`components.exportId`

|

string

|

 _Returned for sharded clusters only._

Unique identifier of the export job for the replica set.  
  
`components.replicaSetName`

|

string

|

 _Returned for sharded clusters only._

Name of the replica set.  
  
`createdAt`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the export job was
created.  
  
`customData`

|

array of documents

|

Custom data for the metadata file named `.complete` that Atlas uploads to the
bucket when the export job finishes.  
  
`customData.key`

|

string

|

Custom data specified as `key` in the key and value pair.  
  
`customData.value`

|

string

|

Value for the key specified using `customData.key`.  
  
`errMsg`

|

string

|

Error message, only if the export job failed.  
  
`exportBucketId`

|

string

|

Unique identifier of the bucket.  
  
`exportStatus`

|

document

|

 _Returned for replica set only._

Status of the export job.  
  
`exportStatus.exportedCollections`

|

int

|

 _Returned for replica set only._

Number of collections that have been exported.  
  
`exportStatus.totalCollections`

|

int

|

 _Returned for replica set only._

Total number of collections to export.  
  
`finishedAt`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the export job
completes.  
  
`id`

|

string

|

Unique identifier of the export job.  
  
`prefix`

|

string

|

Full path on the cloud provider bucket to the folder where the snapshot is
exported. The path is in the following format:

    
    
    | /exported_snapshots/{ORG-NAME}/{PROJECT-NAME}/{CLUSTER-NAME}/{SNAPSHOT-INITIATION-DATE}/{TIMESTAMP}  
      
  
`snapshotId`

|

string

|

Unique identifier of the snapshot.  
  
`state`

|

string

|

Status of the export job. Value can be one of the following:

  * `Queued` \- indicates that the export job is queued

  * `InProgress` \- indicates that the snapshot is being exported

  * `Successful` \- indicates that the export job has completed successfully

  * `Failed` \- indicates that the export job has failed

  
  
## Example Request

    
    
    1| curl --user "{publicApiKey}:{privateApiKey}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --include \  
    5|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/exports/" \  
    6|      --data '{  
    7|               "snapshotId" : "{SNAPSHOT-ID}",  
    8|                 "exportBucketId" : "{BUCKET-ID}",  
    9|                 "customData": [  
    10|                   {  
    11|                     "key": "exported by",  
    12|                     "value": "myName"  
    13|                   }  
    14|                ]  
    15|             }'  
  
## Example Response

Replica Set

Sharded Cluster

    
    
    {  
      
      "createdAt": "2021-05-04T14:43:40Z",  
      "customData": [  
        {  
          "key": "exported by",  
          "value": "myName"  
        }  
      ],  
      "exportBucketId": "604f6322dc786a5341d4f7fb",  
      "exportStatus": {  
        "exportedCollections": 0,  
        "totalCollections": 0  
      },  
      "id": "60915d9cef8ca80cd31646e5",  
      "prefix": "exported_snapshots/KS+Sandbox/mySbx/testCluster/2021-03-27T1409/1620139419",  
      "snapshotId": "605f3bdf16d634087d0e15ce",  
      "state": "Queued"  
    }  
  
What is MongoDB Atlas? →

