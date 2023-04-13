Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Cloud Backup Snapshot Export Jobs

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `/backup/exports` resource enables you to retrieve all backup snapshot
export jobs associated with the specified Atlas cluster.

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

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/exports/  
      
  
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

This endpoint doesn't use HTTP request body parameters.

## Response

### Response Document

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
  
### results Embedded Document

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
    5|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/exports/"  
  
## Example Response

Replica Set

Sharded Cluster

    
    
    {  
      
      "links": [  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/exports/?pageNum=1&itemsPerPage=100",  
          "rel": "self"  
        }  
      ],  
      "results": [  
        {  
          "createdAt": "2021-03-25T16:49:23Z",  
          "exportBucketId": "{BUCKET-ID}",  
          "id": "605ccba3c1c7613f423e1585",  
          "prefix": "/exported_snapshots/{ORG-NAME}/{PROJECT-NAME}/{CLUSTER-NAME}/2021-03-25T1649+0000/1616694179",  
          "snapshotId": "{SNAPSHOT-ID}",  
          "state": "InProgress"  
        }  
      ],  
      "totalCount": 1  
    }  
  
What is MongoDB Atlas? →

