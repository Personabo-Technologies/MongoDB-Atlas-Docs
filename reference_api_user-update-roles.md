Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update Roles for One User

Share Feedback

On this page

  * Resource
  * Required Roles
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

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Add, update, or remove one Atlas user's roles within an organization or
project.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    PATCH /users/{USER-ID}  
      
  
## Required Roles

You must have the appropriate Owner roles to use this API endpoint.

Level

|

Needed Role  
  
|  
  
Organization

|

`Organization Owner`  
  
Project

|

`Project Owner`  
  
## Important

You can always update your own Atlas user account.

If you own an organization or project, you can update the user roles for any
user with membership in that organization or project. You cannot modify any
other user profile information.

### Request Path Parameters

Name

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

Unique 24-hexadecimal digit string that identifies the Atlas user whose roles
you want to update.  
  
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
  
roles

|

array of objects

|

Required

|

Role assigned to the Atlas user.  
  
roles.orgId

|

string

|

Optional

|

Unique 24-hexadecimal digit string that identifies the organization in which
the Atlas user has the specified role.  
  
roles.groupId

|

string

|

Optional

|

Unique 24-hexadecimal digit string that identifies the project in which the
Atlas user has the specified role.  
  
roles.roleName

|

string

|

Required

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

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --include \  
    5|      --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/users/{USER-ID}" \  
    6|      --data '  
    7|        {  
    8|           "roles": [{  
    9|             "groupId": "{GROUP-ID}",  
    10|             "roleName": "{ROLE}"  
    11|          }]  
    12|        }'  
  
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
    2|   "id": "{USER-ID}",  
    3|   "username": "jane",  
    4|   "emailAddress": "jane@qa.example.com",  
    5|   "firstName": "Jane",  
    6|   "lastName": "D'oh",  
    7|   "links": [{  
    8|     "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/{USER-ID}",  
    9|     "rel": "self"  
    10|   },  
    11|   {  
    12|      "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/{USER-ID}/whitelist",  
    13|     "rel": "http://mms.mongodb.com/whitelist"  
    14|   }],  
    15|   "roles": [{  
    16|     "orgId": "{ORG-ID}",  
    17|     "roleName": "ORG_MEMBER"  
    18|   },{  
    19|     "groupId": "{PROJECT-ID}",  
    20|     "roleName": "GROUP_READ_ONLY"  
    21|   }],  
    22|   "teamIds": []  
    23| }  
  
What is MongoDB Atlas? →

