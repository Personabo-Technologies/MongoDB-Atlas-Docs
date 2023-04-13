Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Organization API Keys

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
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

    
    
    GET /orgs/{ORG-ID}/apiKeys  
      
  
### Request Path Parameters

Name

|

Type

|

Description  
  
||  
  
`ORG-ID`

|

string

|

The unique identifier for the organization whose API Keys you want to
retrieve. Use the /orgs endpoint to retrieve all organizations to which the
authenticated user has access.  
  
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

Each **result** is one API key.

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

Description of this Organization API key.  
  
`id`

|

string

|

Unique identifier for this Organization API key.  
  
`links`

|

string

|

An array of documents, representing a link to one or more sub-resources and/or
related resources such as list pagination. See Linking for more information.  
  
`privateKey`

|

string

|

Redacted Private key for this Organization API key.

## Note

### This key displays unredacted when first created.  
  
`publicKey`

|

string

|

Public key for this Organization API key.  
  
`roles`

|

object array

|

Roles that this Organization API key has. This array returns all the
Organization and Project roles the user has in Atlas.  
  
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

If this is an `roles.orgId` (organization), values include:

  * `ORG_OWNER`

  * `ORG_MEMBER`

  * `ORG_GROUP_CREATOR`

  * `ORG_BILLING_ADMIN`

  * `ORG_READ_ONLY`

 **Project Roles**

If this is a `roles.groupId` (project), values include:

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
    2|  --header "Accept: application/json" \  
    3|  --header "Content-Type: application/json" \  
    4|  --include \  
    5|  --request GET "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys?pretty=true"  
  
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
    3|     "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5980cfc70b6d97029d82e3f6/apiKeys?pretty=true&pageNum=1&itemsPerPage=100",  
    4|     "rel" : "self"  
    5|   } ],  
    6|   "results" : [ {  
    7|     "desc" : "Test Docs Service User",  
    8|     "id" : "5c47503320eef5699e1cce8d",  
    9|     "links" : [ {  
    10|       "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5980cfc70b6d98829d82e3f6/apiKeys/5c47503ae0eef5699e1cce8d",  
    11|       "rel" : "self"  
    12|     } ],  
    13|     "privateKey" : "********-****-****-db2c132ca78d",  
    14|     "publicKey" : "{PUBLIC-KEY}",  
    15|     "roles" : [ {  
    16|       "groupId" : "5898b95f87d9d6270e8995d9",  
    17|       "roleName" : "GROUP_OWNER"  
    18|     }, {  
    19|       "groupId" : "5898b95f87d9d6270e8995d9",  
    20|       "roleName" : "GROUP_READ_ONLY"  
    21|     }, {  
    22|       "orgId" : "5980cfc70b6d97029d82e3f6",  
    23|       "roleName" : "ORG_MEMBER"  
    24|     } ]  
    25|   } ],  
    26|   "totalCount" : 1  
    27| }  
  
What is MongoDB Atlas? →

