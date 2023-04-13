Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Request to Download One M2/M5 Cluster Snapshot

Share Feedback

On this page

  * Syntax
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

Request to download a single snapshot from a specified `M2` or `M5` shared
cluster. This endpoint returns a `snapshotURL` which you can use to download
the snapshot. The URL remains active for 4 hours after you make the request.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/download  
      
  
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

Name of the Atlas cluster that contains the snapshot you want to download.  
  
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

Path Element

|

Description  
  
|  
  
`snapshotId`

|

Unique identifier of the snapshot you want to download.  
  
## Response

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

Type of snapshot delivery type. Will always be `DOWNLOAD`.  
  
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

Unique identifier of the source Atlas project.  
  
`restoreFinishedDate`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when the restore job
completed.  
  
`restoreScheduledDate`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when the snapshot restore is
scheduled to take place.  
  
`snapshotFinishedDate`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when Atlas marked the
snapshot associated as `COMPLETED`.  
  
`snapshotId`

|

string

|

Unique identifier of the snapshot.  
  
`snapshotUrl`

|

string

|

URL for the compressed snapshot files for manual download.  
  
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
      --header "Content-Type: application/json" \  
      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/571c390a7cea7e4dbf32b625/clusters/M2AWS/backup/tenant/download" \  
      --data '{"snapshotId": "5d03a6a12a9c4336c3d98d51"}'  
  
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
      
      "clusterName": "M2AWS",  
      "deliveryType": "DOWNLOAD",  
      "expirationDate": "2019-06-14T18:03:00Z",  
      "id": "5d03a9142a9c4336c3d99c79",  
      "projectId": "571c390a7cea7e4dbf32b625",  
      "restoreFinishedDate": "2019-06-14T14:03:00Z",  
      "restoreScheduledDate": "2019-06-14T14:03:00Z",  
      "snapshotFinishedDate": "2019-06-14T14:02:31Z",  
      "snapshotId": "5d03a6a12a9c4336c3d98d51",  
      "snapshotUrl": "{SNAPSHOT-URL}",  
      "status": "COMPLETED",  
      "targetDeploymentItemName": "M2AWS",  
      "targetProjectId": "571c390a7cea7e4dbf32b625"  
    }  
  
What is MongoDB Atlas? →

