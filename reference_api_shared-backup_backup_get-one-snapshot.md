Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Snapshot for an M2/M5 Cluster

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

Retrieve a single snapshot for a specified `M2` or `M5` shared cluster.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/snapshots/{SNAPSHOT-ID}  
      
  
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

Name of the Atlas cluster that contains the snapshot to retrieve.  
  
`SNAPSHOT-ID`

|

Unique identifier of the snapshot to retrieve.  
  
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

This endpoint does not use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
`finishTime`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when Atlas marked the
snapshot as `COMPLETED`.  
  
`id`

|

objectId

|

Unique identifier of the snapshot.  
  
`mongoDBVersion`

|

string

|

Version of the MongoDB server.  
  
`scheduledTime`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when the snapshot is
scheduled to be taken.  
  
`startTime`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when Atlas began taking the
snapshot.  
  
`status`

|

string

|

Current status of the snapshot. Possible values are:

  * `COMPLETED`

  * `FAILED`

  * `PENDING`

  * `QUEUED`

  * `RUNNING`

  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b69d0349b15c62cdfc38b78/clusters/M2AWS/backup/tenant/snapshots/5cc310ace5dc7ce369814bc8"  
  
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
      
      "finishTime" : "2019-04-26T14:08:07Z",  
      "id" : "5cc310ace5dc7ce369814bc8",  
      "mongoDBVersion" : "4.2.7",  
      "scheduledTime" : "2019-04-26T12:00:00Z",  
      "startTime" : "2019-04-26T14:07:53Z",  
      "status" : "FAILED"  
    }  
  
What is MongoDB Atlas? →

