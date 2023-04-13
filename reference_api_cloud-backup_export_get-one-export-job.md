Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Cloud Backup Snapshot Export Job

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

The `/backup/exports` resource enables you to retrieve one backup snapshot
export job specified by its ID.

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

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/exports/{EXPORT-JOB-ID}  
      
  
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
the Atlas cluster whose export job you want to retrieve.  
  
CLUSTER-NAME

|

string

|

Required

|

Name of the Atlas cluster whose export job you want to retrieve.  
  
EXPORT-JOB-ID

|

string

|

Required

|

Unique identifier of the export job to retrieve. If necessary, use Get All
Cloud Backup Snapshot Export Jobs to retrieve the list of export jobs for the
cluster.  
  
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
    5|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/exports/{EXPORT-JOB-ID}"  
  
## Example Response

Replica Set

Sharded Cluster

    
    
    {  
      
      "createdAt": "2021-03-25T16:49:23Z",  
      "exportBucketId": "{BUCKET-ID}",  
      "finishedAt": "2021-03-25T17:48:20Z",  
      "id": "605ccba3c1c7613f423e1585",  
      "prefix": "/exported_snapshots/{ORG-NAME}/{PROJECT-NAME}/{CLUSTER-NAME}/2021-03-25T1649+0000/1616694179",  
      "snapshotId": "605cbac9b498841007af7d9f",  
      "state": "Successful"  
    }  
  
What is MongoDB Atlas? →

