Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get an Atlas User by ID

Share Feedback

On this page

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

Retrieve a Atlas user's profile using their unique identifier. You cannot use
this endpoint to return information on an API Key. To return information on an
API Key, use the Get One API Key endpoint.

## Important

You can always retrieve your own user account.

If you are the owner of an Atlas organization or project, you can also
retrieve the user profile for any user with membership in that organization or
project.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /users/{USER-ID}  
      
  
### Request Path Parameters

Path Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
USER-ID

|

string

|

Required

|

Unique identifier of the user that you want to retrieve. If you know the
user's Atlas username, use the /users/byName/{USER-NAME} endpoint to retrieve
the user's profile and unique identifier.  
  
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

The JSON document contains each of the following elements:

Response Parameter

|

Type

|

Description  
  
||  
  
country

|

string

|

ISO-3166-1 alpha 2 country code of the country in which the Atlas user
resides.  
  
emailAddress

|

string

|

Email address that the Atlas user possesses.  
  
firstName

|

string

|

First or given name that identifies the Atlas user.  
  
id

|

string

|

Unique 24-hexidecimal digit string that identifies the Atlas user.  
  
lastName

|

string

|

Last name, family name, or surname that identifies the Atlas user.  
  
links

|

array

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
mobileNumber

|

string

|

Mobile or cell phone number that the Atlas user possesses.  
  
password

|

string

|

String of eight or more characters that authenticates the Atlas user specified
with **username**. Atlas doesn't return this parameter except in response to
creating a new user.

You can't update the password after it has been created. The user must log
into Atlas to update their password.  
  
roles

|

array

|

List of Atlas Organizations or Projects to which you assigned the Atlas user
_and_ the Atlas role has for the associated organization or project. You can
specify _either_ **roles.orgId** or **roles.groupId** per entry.  
  
roles.groupId

|

string

|

Unique 24-hexidecimal digit string that identifies the project in which the
user has the specified **roles.roleName**.  
  
roles.orgId

|

string

|

Unique 24-hexidecimal digit string that identifies the organization in which
the user has the specified **roles.roleName**.  
  
roles.roleName

|

string

|

Label that identifies the assigned grouping of Atlas privileges.

When associated to **roles.orgId** , the valid roles and their mappings
include:

|

Role

|

Mapping  
  
|  
  
ORG_OWNER

|

`Organization Owner`  
  
ORG_GROUP_CREATOR

|

`Organization Project Creator`  
  
ORG_BILLING_ADMIN

|

`Organization Billing Admin`  
  
ORG_READ_ONLY

|

`Organization Read Only`  
  
ORG_MEMBER

|

`Organization Member`  
  
When associated to **roles.groupId** , the valid roles and their mappings
include:

Role

|

Mapping  
  
|  
  
GROUP_OWNER

|

`Project Owner`  
  
GROUP_CLUSTER_MANAGER

|

`Project Cluster Manager`  
  
GROUP_READ_ONLY

|

`Project Read Only`  
  
GROUP_DATA_ACCESS_ADMIN

|

`Project Data Access Admin`  
  
GROUP_DATA_ACCESS_READ_WRITE

|

`Project Data Access Read/Write`  
  
GROUP_DATA_ACCESS_READ_ONLY

|

`Project Data Access Read Only`  
  
teamIds

|

array

|

Unique identifiers for each team to which the user belongs.  
  
username

|

string

|

Email address that identifies the Atlas user in RFC 5322 format You can't
modify the username after it has been created.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/users/5af1c27a0a7fa48c76d3a761"  
  
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
    2|     "emailAddress": "john.doe@example.com",  
    3|     "firstName": "John",  
    4|     "id": "5af1c27a0a7fa48c76d3a761",  
    5|     "lastName": "Doe",  
    6|     "links": [  
    7|         {  
    8|             "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/5af1c27a0a7fa48c76d3a761",  
    9|             "rel": "self"  
    10|         },  
    11|         {  
    12|             "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/5af1c27a0a7fa48c76d3a761/accessList",  
    13|             "rel": "http://mms.mongodb.com/accessList"  
    14|         }  
    15|     ],  
    16|     "mobileNumber" : "2125550198",  
    17|     "roles": [  
    18|         {  
    19|             "orgId": "5af1c27a0a7fa48c76d3a762",  
    20|             "roleName": "ORG_OWNER"  
    21|         },  
    22|         {  
    23|             "groupId": "5af1c27a0a7fa48c76d3a763",  
    24|             "roleName": "GROUP_OWNER"  
    25|         }  
    26|     ],  
    27|     "teamIds": [  
    28|         "5af1c27a0a7fa48c76d3a764"  
    29|     ],  
    30|     "username": "john.doe@example.com"  
    31| }  
  
What is MongoDB Atlas? →

