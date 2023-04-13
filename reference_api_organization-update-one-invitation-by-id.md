Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update One Organization Invitation by Invitation ID

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

Updates one pending invitation by `{INVITATION-ID}` to the Atlas organization
that you specify.

Use the Get All Organization Invitations endpoint to retrieve IDs for all
pending organization invitations.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You can successfully call this endpoint with the `Organization Owner` role.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    PATCH /orgs/{ORG-ID}/invites/{INVITATION-ID}  
      
  
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

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
roles

|

array of strings

|

Required

|

Atlas roles to assign to the invited user.

If the user accepts the invitation, Atlas assigns these roles to them.

## Important

Atlas replaces the **roles** in the invitation with those that you provide in
this request.

Ensure that you include all roles that you want to assign the user in this
request.  
  
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
         --header "Content-Type: application/json" \  
         --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/invites/{INVITATION-ID}?pretty=true" \  
          --data '  
           {  
              "roles": [  
                "ORG_OWNER"  
              ]  
           }'  
  
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
    2|    "createdAt": "2021-02-18T21:05:40Z",  
    3|    "expiresAt": "2021-03-20T21:05:40Z",  
    4|    "id": "602ed6a49a7b2379719b97f7",  
    5|    "inviterUsername": "admin@example.com",  
    6|    "orgId": "5df7a168f10fab3a149357fb",  
    7|    "orgName": "jww-12-16",  
    8|    "roles": [  
    9|        "ORG_OWNER"  
    10|    ],  
    11|    "teamIds": [],  
    12|    "username": "wyatt.smith@example.com"  
    13| }  
  
What is MongoDB Atlas? →

