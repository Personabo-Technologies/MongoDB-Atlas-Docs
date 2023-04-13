Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create and Assign One Organization API Key to One Project

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

    
    
    POST /groups/{GROUP-ID}/apiKeys  
      
  
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

Unique identifier for the Project whose API keys you want to retrieve. Use the
/groups endpoint to retrieve all organizations to which the authenticated user
has access.  
  
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

At least one of the two body parameters are required.

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`desc`

|

string

|

Conditional

|

Description of the API key. Must be between 1 and 250 characters in length,
inclusive.  
  
`roles`

|

array of strings

|

Conditional

|

List of roles that the API Key needs to have. If you include the `roles`
array:

  * Provide at least one role

  * Make sure all roles must be valid for the Project

Project roles include:

  * `GROUP_CLUSTER_MANAGER`

  * `GROUP_DATA_ACCESS_ADMIN`

  * `GROUP_DATA_ACCESS_READ_ONLY`

  * `GROUP_DATA_ACCESS_READ_WRITE`

  * `GROUP_OWNER`

  * `GROUP_READ_ONLY`

  
  
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
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --include \  
    5|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/apiKeys?pretty=true" \  
    6|      --data '{  
    7|        "desc" : "New API key for test purposes",  
    8|        "roles": ["GROUP_READ_ONLY", "GROUP_DATA_ACCESS_ADMIN"]  
    9|      }'  
  
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
    3|   "id" : "{API-KEY}",  
    4|   "links" : [ {  
    5|     "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY}",  
    6|     "rel" : "self"  
    7|   } ],  
    8|   "privateKey" : "********-****-****-db2c132ca78d",  
    9|   "publicKey" : "{PUBLIC-KEY}",  
    10|   "roles" : [ {  
    11|     "groupId" : "{GROUP-ID}",  
    12|     "roleName" : "GROUP_READ_ONLY"  
    13|   }, {  
    14|     "groupId" : "{GROUP-ID}",  
    15|     "roleName" : "GROUP_DATA_ACCESS_ADMIN"  
    16|   }, {  
    17|     "orgId" : "{ORG-ID}",  
    18|     "roleName" : "ORG_BILLING_ADMIN"  
    19|   } ]  
    20| }  
  
What is MongoDB Atlas? →

