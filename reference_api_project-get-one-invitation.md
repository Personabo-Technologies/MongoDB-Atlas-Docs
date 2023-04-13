Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Project Invitation

Share Feedback

On this page

  * Required Roles
  * Resource
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

Retrieve details for one pending invitation to the specified Atlas project.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You can successfully call this endpoint with the `Project Owner` role.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/invites/{INVITATION-ID}  
      
  
### Request Path Parameters

Path Element

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

Unique 24-hexadecimal digit string that identifies the project.  
  
INVITATION-ID

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the invitation.  
  
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
  
createdAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas sent the
invitation.  
  
expiresAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the invitation expires.

## Tip

Users have 30 days to accept an invitation to an Atlas project.  
  
groupId

|

string

|

Unique 24-hexadecimal digit string that identifies the project.  
  
groupName

|

string

|

Name of the project.  
  
id

|

string

|

Unique 24-hexadecimal digit string that identifies the invitation.  
  
inviterUsername

|

string

|

Atlas user who invited **username** to the project.  
  
roles

|

array of strings

|

Atlas roles to assign to the invited user.

If the user accepts the invitation, Atlas assigns these roles to them.  
  
username

|

string

|

Email address to which Atlas sent the invitation.

If the user accepts the invitation, they use this email address as their Atlas
username.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/invites?pretty=true"  
  
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
    2|   "createdAt": "2021-02-18T18:51:46Z",  
    3|   "expiresAt": "2021-03-20T18:51:46Z",  
    4|   "groupId": "5f0e15e3d52a043fed8b1c92",  
    5|   "groupName": "group",  
    6|   "id": "602eb7429955214668d5b025",  
    7|   "inviterUsername": "admin@example.com",  
    8|   "roles": [  
    9|     "GROUP_OWNER"  
    10|   ],  
    11|   "username": "jane.smith@example.com"  
    12| }  
  
What is MongoDB Atlas? →

