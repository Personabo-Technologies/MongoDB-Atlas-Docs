Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Modify Roles of One Organization API Key to One Project

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

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    PATCH /groups/{GROUP-ID}/apiKeys/{API-KEY-ID}  
      
  
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

Unique identifier for the Project whose API keys you want to update. Use the
/groups endpoint to retrieve all organizations to which the authenticated user
has access.  
  
`API-KEY-ID`

|

string

|

Unique identifier for the API key you want to update. Use the /groups/{GROUP-
ID}/apiKeys endpoint to retrieve all API keys to which the authenticated user
has access for the specified organization.  
  
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

The body parameter is required.

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`roles`

|

string array

|

Required

|

List of roles that the API Key should be granted. A minimum of one role must
be provided. Any roles provided must be valid for the assigned Project:

  * `GROUP_CLUSTER_MANAGER`

  * `GROUP_DATA_ACCESS_ADMIN`

  * `GROUP_DATA_ACCESS_READ_ONLY`

  * `GROUP_DATA_ACCESS_READ_WRITE`

  * `GROUP_OWNER`

  * `GROUP_READ_ONLY`

## Note

Include all roles that you want this API Key to have. Any roles not in this
array are removed.  
  
## Response

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
    2|   --header "Accept: application/json" \  
    3|   --header "Content-Type: application/json" \  
    4|   --include \  
    5|   --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/5953c5f380eef53887615f9a/apiKeys/5d1d143c87d9d63e6d694746?pretty=true" \  
    6|   --data '{  
    7|       "roles": [ "GROUP_READ_ONLY", "GROUP_DATA_ACCESS_READ_WRITE" ]  
    8|     }'  
  
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
    2|   "desc" : "New API key for test purposes",  
    3|   "id" : "5d1d143c87d9d63e6d694746",  
    4|   "links" : [ {  
    5|     "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5980cfe20b6d97029d82fa63/apiKeys/5d1d143c87d9d63e6d694746",  
    6|     "rel" : "self"  
    7|   } ],  
    8|   "privateKey" : "********-****-****-eac4256753ba",  
    9|   "publicKey" : "{PUBLIC-KEY}",  
    10|   "roles" : [ {  
    11|     "orgId" : "5980cfe20b6d97029d82fa63",  
    12|     "roleName" : "ORG_BILLING_ADMIN"  
    13|   }, {  
    14|     "groupId" : "5953c5f380eef53887615f9a",  
    15|     "roleName" : "GROUP_DATA_ACCESS_READ_WRITE"  
    16|   }, {  
    17|     "orgId" : "5980cfe20b6d97029d82fa63",  
    18|     "roleName" : "ORG_MEMBER"  
    19|   }, {  
    20|     "groupId" : "5953c5f380eef53887615f9a",  
    21|     "roleName" : "GROUP_READ_ONLY"  
    22|   } ]  
    23| }  
    24| }  
  
What is MongoDB Atlas? →

