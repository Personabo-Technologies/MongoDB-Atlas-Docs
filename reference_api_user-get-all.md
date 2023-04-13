Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Users in One Project

Share Feedback

On this page

  * Resource
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

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

    
    
    GET /groups/{GROUP-ID}/users  
      
  
## Request Parameters

### Request Path Parameters

Path Parameter

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

Unique identifier for the group.  
  
### Request Query Parameters

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
  
pageNum

|

integer

|

Optional

|

Page number, starting with one, that Atlas returns of the total number of
objects.

|

`1`  
  
itemsPerPage

|

integer

|

Optional

|

Number of items that Atlas returns per page, up to a maximum of 500.

|

`100`  
  
includeCount

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the **totalCount** parameter in the
response body.

|

`true`  
  
pretty

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the JSON response in the prettyprint
format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag that indicates whether Atlas wraps the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

Endpoints that return a list of results use the **results** object as an
envelope. Atlas adds the **status** parameter to the response body.

|

`false`  
  
|

|

|

|  
  
||||  
  
flattenTeams

|

boolean

|

Optional

|

Flag that indicates whether the returned list should include users who belong
to a team that is assigned a role in this project. You might not have assigned
the individual users a role in this project.

  * If this flag is set to `false`, the endpoint returns only users that were assigned a role in the project.

  * If this flag is set to `true`, the endpoint returns both users that were assigned roles in the project _and_ users who are members of teams that were assigned roles in the project.

|

`false`  
  
includeOrgUsers

|

boolean

|

Optional

|

Flag that indicates whether the returned list should include users with
implicit access to the project through the `Organization Owner` or
`Organization Read Only` role. You might not have assigned the individual
users a role in this project.

  * If this flag is set to `false`, the endpoint returns only users who are assigned a role in the project.

  * If this flag is set to `true`, the endpoint returns both users who are assigned roles in the project _and_ users who have implicit access to the project through their organization role.

|

`false`  
  
### Request Body Parameters

This endpoint doesn't use HTTP request body parameters.

## Response

### Response Document

The response JSON document includes an array of **result** objects, an array
of **link** objects and a count of the total number of **result** objects
retrieved.

Name

|

Type

|

Description  
  
||  
  
results

|

array of objects

|

One object for each item detailed in the results Embedded Document section.  
  
links

|

array of objects

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
totalCount

|

integer

|

Count of the total number of items in the result set. It may be greater than
the number of objects in the **results** array if the entire result set is
paginated.  
  
### results Embedded Document

Each **result** is one user.

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

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/users?pretty=true&includeOrgUsers=true"  
  
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
    2|  "links": [{  
    3|    "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/ users?pretty=true&pageNum=1&itemsPerPage=100",  
    4|    "rel": "self"  
    5|  }],  
    6|  "results": [{  
    7|    "country" : "UK",  
    8|    "emailAddress": "joe.bloggs@example.com",  
    9|    "firstName": "Joe",  
    10|    "id": "{USER-ID}",  
    11|    "lastName": "Bloggs",  
    12|    "links": [{  
    13|      "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/{USER-ID}",  
    14|      "rel": "self"  
    15|    }, {  
    16|      "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/{USER-ID}/accessList",  
    17|      "rel": "http://mms.mongodb.com/accessList"  
    18|    }],  
    19|    "roles": [{  
    20|      "groupId": "{GROUP-ID}",  
    21|      "roleName": "GROUP_OWNER"  
    22|    }, {  
    23|      "groupId": "{OTHER-GROUP-ID}",  
    24|      "roleName": "GROUP_OWNER"  
    25|    }],  
    26|    "username": "joe.bloggs"  
    27|  }, {  
    28|    "country" : "UK",  
    29|    "emailAddress": "jim.bloggs@example.com",  
    30|    "firstName": "Jim",  
    31|    "id": "{OTHER-USER-ID}",  
    32|    "lastName": "Bloggs",  
    33|    "links": [{  
    34|      "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/{OTHER-USER-ID}",  
    35|      "rel": "self"  
    36|    }, {  
    37|      "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/{OTHER-USER-ID}/accessList",  
    38|      "rel": "http://mms.mongodb.com/accessList"  
    39|    }],  
    40|    "roles": [{  
    41|      "roleName": "GLOBAL_READ_ONLY"  
    42|    }, {  
    43|      "groupId": "{GROUP-ID}",  
    44|      "roleName": "GROUP_OWNER"  
    45|    }, {  
    46|      "orgId": "{ORGANIZATION-ID}",  
    47|      "roleName": "ORG_READ_ONLY"  
    48|    }],  
    49|    "username": "jim.bloggs"  
    50|  }],  
    51|  "totalCount": 2  
    52| }  
  
What is MongoDB Atlas? →

