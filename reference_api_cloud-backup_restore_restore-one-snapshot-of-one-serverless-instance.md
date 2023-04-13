Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Restore One Snapshot Of One Serverless Instance

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

Restore one snapshot for the specified serverless instance.

## Required Roles

Your API Key must have one of the following roles to successfully call this
resource:

  * `Organization Owner`

  * `Project Owner`

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{groupId}/serverless/{instanceName}/backup/restoreJobs  
      
  
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

Name

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

Type of restore job to create. Atlas returns **automated**.  
  
snapshotId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the source of restore job.  
  
targetClusterName

|

string

|

Required

|

Human-readable label of the target Atlas cluster or serverless instance to
which the restore job restores the snapshot.  
  
targetGroupId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the target Atlas project
for this restore job.  
  
## Response

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

Flag that indicates whether someone canceled the restore job.  
  
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

Type of restore job to create. Atlas returns **automated**.  
  
expired

|

boolean

|

Flag that indicates whether the restore job expired.  
  
expiresAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the restore job
expires.  
  
failed

|

boolean

|

Flag that indicates whether someone canceled the restore job.  
  
finishedAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the restore job
completed.  
  
id

|

string

|

Unique 24-hexadecimal digit string that identifies the restore job.  
  
snapshotId

|

string

|

Unique 24-hexadecimal digit string that identifies the source of restore job.  
  
targetClusterName

|

string

|

Human-readable label of the target Atlas cluster or serverless instance to
which the restore job restores the snapshot.  
  
targetGroupId

|

string

|

Unique 24-hexadecimal digit string that identifies the target Atlas project of
the restore job.  
  
timestamp

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas took the snapshot
identified with **snapshotId**.  
  
## Example Request

    
    
    1| curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
    |  
    2|      --header 'Accept: application/json' \  
    3|      --header 'Content-Type: application/json' \  
    4|      --include \  
    5|      --request POST 'https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName}/backup/restoreJobs?pretty=true' \  
    6|      --data '{  
    7|             "snapshotId": "{snapshotId}",  
    8|             "deliveryType": "automated",  
    9|             "targetGroupId": "{targetGroupId}",  
    10|             "targetClusterName": "{clusterName}"  
    11|          }'  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 201 Created  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    1| {  
    |  
    2|   "cancelled": false,  
    3|   "deliveryType": "automated",  
    4|   "deliveryUrl": [],  
    5|   "expired": false,  
    6|   "expiresAt": "2021-04-20T00:00:00Z",  
    7|   "failed": false,  
    8|   "id": "{snapshotId}",  
    9|   "snapshotId": "{snapshotId}",  
    10|   "targetClusterName": "{clusterName}",  
    11|   "targetDeploymentItemName": "{deploymentName}",  
    12|   "targetGroupId": "{targetGroupId}",  
    13|   "timestamp": "2020-12-21T00:00:00Z"  
    14| }  
  
What is MongoDB Atlas? →

