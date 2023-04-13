Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Restore Job from an M2/M5 Cluster

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

## Important

Restoring a snapshot to a cluster **removes all existing data** on the target
cluster prior to the restore.

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

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/restore  
      
  
### Request Path Parameters

Path Element

|

Description  
  
|  
  
`GROUP-ID`

|

The unique identifier of the project for the Atlas cluster whose snapshot you
want to restore.  
  
`CLUSTER-NAME`

|

The name of the Atlas cluster whose snapshot you want to restore.  
  
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

All listed fields are required.

Name

|

Type

|

Description  
  
||  
  
`snapshotId`

|

objectId

|

Unique identifier of the snapshot to restore.  
  
`targetDeploymentItemName`

|

string

|

Name of the cluster on the target Atlas project to which the restore job
restores the snapshot. You can restore the snapshot to a cluster tier `M2` or
greater.  
  
`targetProjectId`

|

objectId

|

Unique identifier of the target Atlas project to which the restore job
restores the snapshot.  
  
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

Name of the Atlas cluster.  
  
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

Timestamp in ISO 8601 date and time format in UTC point in time when the
restore job expires.  
  
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
  
`restoreScheduledDate`

|

date

|

Timestamp in ISO 8601 date and time format in UTC point in time when the
snapshot restore is scheduled to take place.  
  
`snapshotFinishedDate`

|

date

|

Timestamp in ISO 8601 date and time format in UTC point in time when the
snapshot was taken.  
  
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
      --header "Content-Type: application/json" \  
      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/571c390a7cea7e4dbf32b625/clusters/M2AWS/backup/tenant/restore" \  
      --data '{  
                "snapshotId": "5ced491ce7a2e10517c81fa7",  
                "targetProjectId": "571c390a7cea7e4dbf32b625",  
                "targetDeploymentItemName": "M2AWS"  
              }'  
  
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
      
      "clusterName":"M2AWS",  
      "deliveryType":"RESTORE",  
      "expirationDate":"2019-05-29T13:10:27Z",  
      "id":"5cee4c83e7a2e10d2ad35971",  
      "projectId":"571c390a7cea7e4dbf32b625",  
      "restoreScheduledDate":"2019-05-29T09:10:27Z",  
      "snapshotFinishedDate":"2019-05-28T14:44:01Z",  
      "snapshotId":"5ced491ce7a2e10517c81fa7",  
      "status":"PENDING",  
      "targetDeploymentItemName":"M2AWS",  
      "targetProjectId":"571c390a7cea7e4dbf32b625"  
    }  
  
What is MongoDB Atlas? →

