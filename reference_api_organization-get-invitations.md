Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Organization Invitations

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

Retrieves all pending invitations to the specified Atlas organization.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You can successfully call this endpoint with the `Organization Owner` role.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /orgs/{ORG-ID}/invites  
      
  
### Request Path Parameters

Path Element

|

Type

|

Necessity

|

Description  
  
|||  
  
ORG-ID

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the organization.  
  
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
  
|

|

|

|  
  
||||  
  
username

|

string

|

Optional

|

Email address of the invited user. This is the address to which Atlas sent the
invite.

If omitted, Atlas returns all pending invitations.

|  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

The response JSON document includes an array of objects. Each object
represents one invitation to the Atlas project.

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
  
id

|

string

|

Unique 24-hexadecimal digit string that identifies the invitation.  
  
inviterUsername

|

string

|

Atlas user who invited **username** to the organization.  
  
orgId

|

string

|

Unique 24-hexadecimal digit string that identifies the organization.  
  
orgName

|

string

|

Name of the organization.  
  
roles

|

array of strings

|

Atlas roles to assign to the invited user.

If the user accepts the invitation, Atlas assigns these roles to them.  
  
teamIds

|

array of strings

|

Unique 24-hexadecimal digit strings that identify the teams that the user was
invited to join.  
  
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
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/invites?pretty=true"  
  
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

    
    
    1| [  
    |  
    2|     {  
    3|         "createdAt": "2021-02-18T18:51:46Z",  
    4|         "expiresAt": "2021-03-20T18:51:46Z",  
    5|         "id": "602eb7429955214668d5b025",  
    6|         "inviterUsername": "admin@example.com",  
    7|         "orgId": "5df7a168f10fab3a149357fb",  
    8|         "orgName": "jww-12-16",  
    9|         "roles": [  
    10|             "GROUP_OWNER"  
    11|         ],  
    12|         "teamIds": [],  
    13|         "username": "jane.smith@example.com"  
    14|     },  
    15|     {  
    16|         "createdAt": "2021-02-18T21:28:38Z",  
    17|         "expiresAt": "2021-03-20T21:28:38Z",  
    18|         "id": "602edc067aaadd60360ed46b",  
    19|         "inviterUsername": "admin@example.com",  
    20|         "orgId": "5df7a168f10fab3a149357fb",  
    21|         "orgName": "jww-12-16",  
    22|         "roles": [  
    23|             "ORG_MEMBER"  
    24|         ],  
    25|         "teamIds": [],  
    26|         "username": "john.smith@example.com"  
    27|     },  
    28|     {  
    29|         "createdAt": "2021-02-18T21:05:40Z",  
    30|         "expiresAt": "2021-03-20T21:05:40Z",  
    31|         "id": "602ed6a49a7b2379719b97f7",  
    32|         "inviterUsername": "admin@example.com",  
    33|         "orgId": "5df7a168f10fab3a149357fb",  
    34|         "orgName": "jww-12-16",  
    35|         "roles": [  
    36|             "ORG_MEMBER"  
    37|         ],  
    38|         "teamIds": [],  
    39|         "username": "wyatt.smith@example.com"  
    40|     }  
    41| ]  
  
What is MongoDB Atlas? →

