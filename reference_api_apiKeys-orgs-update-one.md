Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update One Organization API Key

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

    
    
    PATCH /orgs/{ORG-ID}/apiKeys/{API-KEY-ID}  
      
  
### Request Path Parameters

All path parameters are required.

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`ORG-ID`

|

string

|

Required

|

Unique identifier for the organization whose API keys you want to retrieve.
Use the /orgs endpoint to retrieve all organizations to which the
authenticated user has access.  
  
`API-KEY-ID`

|

string

|

Required

|

Unique identifier for the API key you want to update. Use the /orgs/{ORG-
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

The request must contain either a `desc` or a `roles` parameter.

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

Optional

|

Description of the key. If `desc` is provided, it must be between 1 and 250
characters long.  
  
`roles`

|

string array

|

Optional

|

List of roles that the API Key needs to have. If the `roles` array is
provided:

  * Provide at least one role

  * Make sure all roles must be valid for the Organization

The Organization roles are:

  * `ORG_OWNER`

  * `ORG_MEMBER`

  * `ORG_GROUP_CREATOR`

  * `ORG_BILLING_ADMIN`

  * `ORG_READ_ONLY`

  
  
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
    2|   --header "Accept: application/json" \  
    3|   --header "Content-Type: application/json" \  
    4|   --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}?pretty=true" \  
    5|   --data '{  
    6|     "desc" : "Updated API key description for test purposes",  
    7|     "roles": ["ORG_MEMBER", "ORG_READ_ONLY"]  
    8|   }'  
  
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
    2|   "desc" : "Updated API key description for test purposes",  
    3|   "id" : "5c47ba5127d9d61b9fd8a27b",  
    4|   "links" : [ {  
    5|     "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5980cfc70b6d12029d82e3f6/apiKeys/5c47ba5127d9d61b9fd8a27b",  
    6|     "rel" : "self"  
    7|   } ],  
    8|   "privateKey" : "********-****-****-db2c132ca78d",  
    9|   "publicKey" : "{PUBLIC-KEY}",  
    10|   "roles" : [ {  
    11|     "orgId" : "5980cfc70b6d97029d82e3f6",  
    12|     "roleName" : "ORG_MEMBER"  
    13|   }, {  
    14|     "orgId" : "5980cfc70b6d97029d82e3f6",  
    15|     "roleName" : "ORG_READ_ONLY"  
    16|   } ]  
    17| }  
  
What is MongoDB Atlas? →

