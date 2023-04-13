Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Organization API Keys Assigned to One Project

Share Feedback

On this page

  * Resource
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

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/apiKeys  
      
  
### Request Path Parameters

Name

|

Type

|

Description  
  
||  
  
`GROUP-ID`

|

string

|

Unique identifier for the Project from which you want to retrieve its assigned
Organization API keys. Use the /groups endpoint to retrieve all Projects to
which the authenticated user has access.  
  
### Request Query Parameters

This endpoint may use any of the HTTP request query parameters available to
all Atlas Administration API resources. These are all optional.

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

Each **result** is one Project API key.

Name

|

Type

|

Description  
  
||  
  
`desc`

|

string

|

Description of this Organization API key assigned to this Project.  
  
`id`

|

string

|

Unique identifier for this Organization API key assigned to this Project.  
  
`privateKey`

|

string

|

Redacted Private key for this Organization API key assigned to this Project.

## Note

### This key displays unredacted when first created.  
  
`publicKey`

|

string

|

Public key for this Organization API key assigned to this Project.  
  
`roles`

|

array of objects

|

Roles that this Organization API key assigned to this Project has. This array
returns all the Organization and Project roles the user has in Atlas.  
  
`roles.groupId`

|

string

|

Unique identifier of the Project to which this role belongs.  
  
`roles.orgId`

|

string

|

Unique identifier of the Organization to which this role belongs.  
  
`roles.roleName`

|

string

|

Name of the role. This resource returns all the roles the user has in Atlas.
Possible values are:

 **Organization Roles**

If this is an `roles.orgId` (Organization), values include:

  * `ORG_OWNER`

  * `ORG_MEMBER`

  * `ORG_GROUP_CREATOR`

  * `ORG_BILLING_ADMIN`

  * `ORG_READ_ONLY`

 **Project Roles**

If this is an `roles.groupId` (Project), values include:

  * `GROUP_CLUSTER_MANAGER`

  * `GROUP_DATA_ACCESS_ADMIN`

  * `GROUP_DATA_ACCESS_READ_ONLY`

  * `GROUP_DATA_ACCESS_READ_WRITE`

  * `GROUP_OWNER`

  * `GROUP_READ_ONLY`

  
  
## Example Request

## Note

The user who makes the request can be formatted either as
`{USERNAME}:{APIKEY}` or `{PUBLIC-KEY}:{PRIVATE-KEY}`.

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --include \  
    4|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/5953c5f380eef53887615f9a/apiKeys?pretty=true"  
  
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
    2|   "links" : [ {  
    3|     "href" : "https://cloud.mongodb.com/api/public/v1.0/groups/5953c5f380eef53887615f9a/apiKeys?pretty=true&pageNum=1&itemsPerPage=100",  
    4|     "rel" : "self"  
    5|   } ],  
    6|   "results" : [ {  
    7|     "desc" : "Updated API Key description for DOCSP-6042",  
    8|     "id" : "5d1cf1f980eef570c9fc87e5",  
    9|     "links" : [ {  
    10|       "href" : "https://cloud.mongodb.com/api/public/v1.0/orgs/5980cfe20b6d97029d82fa63/apiKeys/5d1cf1f980eef570c9fc87e5",  
    11|       "rel" : "self"  
    12|     } ],  
    13|     "privateKey" : "********-****-****-9d4ae38e4ddd",  
    14|     "publicKey" : "{PUBLIC-KEY}",  
    15|     "roles" : [ {  
    16|       "groupId" : "5953c5f380eef53887615f9a",  
    17|       "roleName" : "GROUP_AUTOMATION_ADMIN"  
    18|     }, {  
    19|       "groupId" : "5953c5f380eef53887615f9a",  
    20|       "roleName" : "GROUP_MONITORING_ADMIN"  
    21|     }, {  
    22|       "orgId" : "5980cfe20b6d97029d82fa63",  
    23|       "roleName" : "ORG_MEMBER"  
    24|     }, {  
    25|       "orgId" : "5980cfe20b6d97029d82fa63",  
    26|       "roleName" : "ORG_BILLING_ADMIN"  
    27|     }, {  
    28|       "groupId" : "5953c5f380eef53887615f9a",  
    29|       "roleName" : "GROUP_DATA_ACCESS_ADMIN"  
    30|     }, {  
    31|       "groupId" : "5953c5f380eef53887615f9a",  
    32|       "roleName" : "GROUP_USER_ADMIN"  
    33|     }, {  
    34|       "groupId" : "5953c5f380eef53887615f9a",  
    35|       "roleName" : "GROUP_READ_ONLY"  
    36|     }, {  
    37|       "groupId" : "5953c5f380eef53887615f9a",  
    38|       "roleName" : "GROUP_OWNER"  
    39|     }, {  
    40|       "orgId" : "5980cfe20b6d97029d82fa63",  
    41|       "roleName" : "ORG_OWNER"  
    42|     }, {  
    43|       "groupId" : "5953c5f380eef53887615f9a",  
    44|       "roleName" : "GROUP_DATA_ACCESS_READ_WRITE"  
    45|     }, {  
    46|       "orgId" : "5980cfe20b6d97029d82fa63",  
    47|       "roleName" : "ORG_GROUP_CREATOR"  
    48|     }, {  
    49|       "orgId" : "5980cfe20b6d97029d82fa63",  
    50|       "roleName" : "ORG_READ_ONLY"  
    51|     }, {  
    52|       "groupId" : "5953c5f380eef53887615f9a",  
    53|       "roleName" : "GROUP_DATA_ACCESS_READ_ONLY"  
    54|     }, {  
    55|       "groupId" : "5953c5f380eef53887615f9a",  
    56|       "roleName" : "GROUP_BACKUP_ADMIN"  
    57|     }, {  
    58|       "groupId" : "5953c5f380eef53887615f9a",  
    59|       "roleName" : "GROUP_CLUSTER_MANAGER"  
    60|     } ]  
    61|   }, {  
    62|     "desc" : "New API key for test purposes",  
    63|     "id" : "5d1d12c087d9d63e6d682438",  
    64|     "links" : [ {  
    65|       "href" : "https://cloud.mongodb.com/api/public/v1.0/orgs/5980cfe20b6d97029d82fa63/apiKeys/5d1d12c087d9d63e6d682438",  
    66|       "rel" : "self"  
    67|     } ],  
    68|     "privateKey" : "********-****-****-cb34f12aafdb",  
    69|     "publicKey" : "oxhzytwb",  
    70|     "roles" : [ {  
    71|       "groupId" : "5953c5f380eef53887615f9a",  
    72|       "roleName" : "GROUP_READ_ONLY"  
    73|     }, {  
    74|       "orgId" : "5980cfe20b6d97029d82fa63",  
    75|       "roleName" : "ORG_MEMBER"  
    76|     }, {  
    77|       "orgId" : "5980cfe20b6d97029d82fa63",  
    78|       "roleName" : "ORG_BILLING_ADMIN"  
    79|     } ]  
    80|   } ],  
    81|   "totalCount" : 2  
    82| }  
  
What is MongoDB Atlas? →

