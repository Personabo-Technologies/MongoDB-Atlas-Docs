Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create an Atlas User

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

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The following resource creates a new Atlas user and assigns it to one or more
of your Atlas projects and organizations.

## Note

Atlas sends an email to the selected users inviting them to join the project.
Invited users do not have access to the project until they accept the
invitation. Invitations expire after 30 days.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Important

Atlas limits Atlas user membership to a maximum of 250 Atlas users per team.

Atlas limits Atlas user membership to 500 Atlas users per project and 500
Atlas users per organization, which includes the combined membership of all
projects in the organization.

Atlas raises an error if an operation exceeds these limits.

## Example

You have an organization with five projects. Each project has 100 Atlas users.
Each Atlas user belongs to only one project. You cannot add any Atlas users to
this organization without first removing existing Atlas users from the
organization membership.

Create a new user.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /users  
      
  
### Request Path Parameters

This endpoint does not use HTTP request path parameters.

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
  
country

|

string

|

Required

|

ISO-3166-1 alpha 2 country code of the country in which the Atlas user
resides.  
  
emailAddress

|

string

|

Required

|

Email address that the Atlas user possesses.  
  
firstName

|

string

|

Required

|

First or given name that identifies the Atlas user.  
  
lastName

|

string

|

Required

|

Last name, family name, or surname that identifies the Atlas user.  
  
mobileNumber

|

string

|

Optional

|

Mobile or cell phone number that the Atlas user possesses.  
  
password

|

string

|

Required

|

String of eight or more characters that authenticates the Atlas user specified
with **username**.

## Note

### Atlas Password Policy

Your Atlas **user account** password must:

  * Contain at least eight characters.

  * Contain unique characters, numbers, or symbols.

  * Exclude your email address and Atlas username.

  * Differ from your previous four passwords.

  * Differ from the most commonly used passwords.

You can't update the password after it has been created. The user must log
into Atlas to update their password.  
  
roles

|

array

|

Required

|

List of Atlas Organizations or Projects to which you assigned the Atlas user
_and_ the Atlas role has for the associated organization or project. You can
specify _either_ **roles.orgId** or **roles.groupId** per entry.  
  
roles.groupId

|

string

|

Required

|

Unique 24-hexidecimal digit string that identifies the project in which the
user has the specified **roles.roleName**.  
  
roles.orgId

|

string

|

Required

|

Unique 24-hexidecimal digit string that identifies the organization in which
the user has the specified **roles.roleName**.  
  
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
  
username

|

string

|

Required

|

Email address that identifies the Atlas user in RFC 5322 format You can't
modify the username after it has been created.  
  
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

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/users/" \  
    5|      --data '  
    6|        {  
    7|          "username" : "john.doe@example.com",  
    8|          "password" : "myPassword1@",  
    9|          "emailAddress" : "john.doe@example.com",  
    10|          "mobileNumber" : "2125550198",  
    11|          "firstName" : "John",  
    12|          "lastName" : "Doe",  
    13|          "roles" : [  
    14|            {  
    15|              "orgId" : "8dbbe4570bd55b23f25444db",  
    16|              "roleName" : "ORG_MEMBER"  
    17|            },  
    18|            {  
    19|              "groupId" : "2ddoa1233ef88z75f64578ff",  
    20|              "roleName" : "GROUP_READ_ONLY"  
    21|            }  
    22|          ],  
    23|          "country" : "US"  
    24|        }'  
  
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
    2|   "emailAddress": "john.doe@example.com",  
    3|   "firstName": "John",  
    4|   "id": "5b06ed7083fb5a40df86e93b",  
    5|   "lastName": "Doe",  
    6|   "links": [  
    7|     {  
    8|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/5b06ed7083fb5a40df86e93b",  
    9|       "rel": "self"  
    10|     },  
    11|     {  
    12|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/5b06ed7083fb5a40df86e93b/accessList",  
    13|       "rel": "http://mms.mongodb.com/accessList"  
    14|     }  
    15|   ],  
    16|   "mobileNumber" : "2125550198",  
    17|   "roles": [],  
    18|   "teamIds": [],  
    19|   "username": "john.doe@example.com"  
    20| }  
  
What is MongoDB Atlas? →

