Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Restore Jobs for an M2/M5 Cluster

Share Feedback

On this page

  * Syntax
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

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Retrieve all snapshot restore jobs for a specified `M2` or `M5` shared
cluster.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/restores  
      
  
### Request Path Parameters

Path Element

|

Description  
  
|  
  
`GROUP-ID`

|

Unique identifier of the project for the Atlas cluster.  
  
`CLUSTER-NAME`

|

Name of the Atlas cluster for which you want to retrieve restore jobs.  
  
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
  
`clusterName`

|

string

|

Name of the source Atlas cluster.  
  
`deliveryType`

|

string

|

Type of restore job to create. Possible values are:

|

Value

|

Description  
  
|  
  
`RESTORE`

|

Atlas automatically restores the snapshot with `snapshotId` to the Atlas
cluster with name `targetDeploymentItemName` in the Atlas project with
`targetProjectId`.  
  
`DOWNLOAD`

|

Atlas provides a URL to download a `.tar.gz` of the snapshot with
`snapshotId`. The contents of the archive contain the data files for your
Atlas cluster. To learn more about manually restoring the downloaded data
files, see Procedure.  
  
`expirationDate`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when the download link
expires.  
  
`id`

|

objectId

|

Unique identifier of the restore job.  
  
`projectId`

|

objectId

|

Unique identifier of the Atlas project from which the restore job originated.  
  
`restoreFinishedDate`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when Atlas marked the
restore job as `COMPLETED`.  
  
`restoreScheduledDate`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when the restore was
requested.  
  
`snapshotFinishedDate`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when the snapshot associated
with `snapshotId` was marked as `COMPLETED`.  
  
`snapshotId`

|

string

|

Unique identifier of the source snapshot ID of the restore job.  
  
`snapshotUrl`

|

string

|

URL for the compressed snapshot files for manual download. Only visible if
`deliveryType` is `DOWNLOAD`.  
  
`status`

|

string

|

Current status of the restore job. Possible values are:

  * `COMPLETED`

  * `FAILED`

  * `PENDING`

  * `QUEUED`

  * `RUNNING`

  
  
`targetDeploymentItemName`

|

string

|

Name of the target Atlas project of the restore job.  
  
`targetProjectId`

|

string

|

Unique identifier of the Atlas project to which the restore job restores the
snapshot.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b69d0349b15c62cdfc38b78/clusters/aws-cluster-1/backup/tenant/restores"  
  
## Example Response

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
      
    
    {  
      
      "results" : [ {  
        "clusterName" : "aws-cluster-1",  
        "deliveryType" : "DOWNLOAD",  
        "expirationDate" : "2019-05-01T19:02:25Z",  
        "finishedDate" : "2019-05-01T15:02:25Z",  
        "id" : "5cc9b501e5dc7c8ab1e45d65",  
        "projectId" : "5b69d0349b15c62cdfc38b78",  
        "snapshotId" : "5cc9ad92e5dc7c8ab1e41c50",  
        "snapshotUrl" : "{SNAPSHOT-URL}",  
        "status" : "COMPLETED",  
        "submittedAt" : "2019-05-01T15:02:25Z",  
        "targetDeploymentItemName" : "aws-cluster-1",  
        "targetProjectId" : "5b69d0349b15c62cdfc38b78",  
        "timestamp" : "2019-05-01T14:33:19Z"  
      }, {  
        "clusterName" : "aws-cluster-1",  
        "deliveryType" : "RESTORE",  
        "expirationDate" : "2019-05-01T18:34:19Z",  
        "id" : "5cc9ae6be5dc7c8ab1e422df",  
        "projectId" : "5b69d0349b15c62cdfc38b78",  
        "snapshotId" : "5cc9ad92e5dc7c8ab1e41c50",  
        "status" : "PENDING",  
        "submittedAt" : "2019-05-01T14:34:19Z",  
        "targetDeploymentItemName" : "aws-cluster-1",  
        "targetProjectId" : "5b69d0349b15c62cdfc38b78",  
        "timestamp" : "2019-05-01T14:33:19Z"  
      } ],  
      "totalCount" : 2  
    }  
  
What is MongoDB Atlas? →

