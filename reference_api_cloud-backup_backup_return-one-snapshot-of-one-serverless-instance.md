Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return One Snapshot Of One Serverless Instance

Share Feedback

On this page

  * Required Roles
  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Return one snapshot of one serverless instance from the specified project.

## Required Roles

Your API Key must have the `Project Read Only` role to successfully call this
resource.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{groupId}/serverless/{instanceName}/backup/snapshots/{snapshotId}  
      
  
### Request Path Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
groupId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies your project.  
  
instanceName

|

string

|

Required

|

Human-readable label that identifies your serverless instance.  
  
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
  
createdAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas took the
snapshot. Atlas sorts the **results** document in descending order based on
this date.  
  
expiresAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas deletes the
snapshot.  
  
id

|

string

|

Unique 24-hexadecimal digit string that identifies your snapshot.  
  
mongodVersion

|

string

|

Version of the MongoDB server.  
  
serverlessInstanceName

|

string

|

Human-readable label given to the serverless instance from which Atlas took
this snapshot.  
  
snapshotType

|

string

|

Type of snapshot. Atlas returns **scheduled**.  
  
status

|

string

|

Current status of the snapshot. Atlas can return one of the following values:

  *  **queued**

  *  **inProgress**

  *  **completed**

  *  **failed**

  
  
storageSizeBytes

|

integer

|

Size of the snapshot in bytes.  
  
## Example Request

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
         --header 'Content-Type: application/json' \  
         --include \  
         --request GET 'https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName}/backup/snapshots/{snapshotId}?pretty=true'  
  
## Example Response

### Response Header

    
    
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
  
### Response Body

    
    
    1| {  
    |  
    2|   "createdAt": "2020-12-20T00:00:00Z",  
    3|   "expiresAt": "2021-02-19T21:04:52Z",  
    4|   "id": "{snapshotId}",  
    5|   "mongodVersion": "5.0.0",  
    6|   "serverlessInstanceName": "{instanceName}",  
    7|   "snapshotType": "scheduled",  
    8|   "status": "completed",  
    9|   "storageSizeBytes": 1024  
    10| }  
  
What is MongoDB Atlas? →

