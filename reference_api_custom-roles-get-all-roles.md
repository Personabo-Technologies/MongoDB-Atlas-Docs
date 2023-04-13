Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Custom Roles in a Project

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Request
  * Response
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

`https://cloud.mongodb.com/api/atlas/v1.0`

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Syntax

    
    
    GET /groups/{GROUP-ID}/customDBRoles/roles  
      
  
### Request Path Parameters

Parameter

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required.

|

The unique identifier for the project.  
  
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

This endpoint does not use HTTP request body parameters.

### Response Elements

If you set the query element `envelope` to `true`, the response is wrapped by
the `content` object.

The HTTP response returns an array of JSON documents, each representing a
custom role. Each document in the array contains the following fields:

Name

|

Type

|

Description  
  
||  
  
`actions`

|

array

|

Each object in the `actions` array represents an individual privilege action
granted by the role.  
  
`actions.action`

|

string

|

Name of the privilege action. For a complete list of actions available in the
Atlas Administration API, see Custom Role Actions.  
  
`actions.resources`

|

array

|

Contains information on where the action is granted. Each object in the array
either indicates a database and collection on which the action is granted, or
indicates that the action is granted on the cluster resource.  
  
`actions.resources.collection`

|

string

|

Collection on which the action is granted. If this value is an empty string,
the action is granted on all collections within the database specified in the
`actions.resources.db` field.

## Note

This field is mutually exclusive with the `actions.resources.cluster` field.  
  
`actions.resources.db`

|

string

|

Database on which the action is granted.

## Note

This field is mutually exclusive with the `actions.resources.cluster` field.  
  
`actions.resources.cluster`

|

boolean

|

Set to `true` to indicate that the action is granted on the cluster resource.

## Note

This field is mutually exclusive with the `actions.resources.collection` and
`actions.resources.db` fields.  
  
`inheritedRoles`

|

array

|

Each object in the `inheritedRoles` array represents a key-value pair
indicating the inherited role and the database on which the role is granted.  
  
`inheritedRoles.db`

|

string

|

Database on which the inherited role is granted.  
  
`inheritedRoles.role`

|

string

|

Name of the inherited role. This can either be another custom role or a built-
in role.  
  
`roleName`

|

string

|

Name of the custom role.  
  
## Example Request

### Request

## Important

You must modify the following code block with the appropriate credentials and
project ID.

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
     --header 'Accept: application/json' \  
     --include \  
     --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/customDBRoles/roles?pretty=true"  
  
### Response

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

    
    
    1| [ {  
    |  
    2|   "actions" : [ ],  
    3|   "inheritedRoles" : [ {  
    4|     "db" : "test",  
    5|     "role" : "readWrite"  
    6|   }, {  
    7|     "db" : "test",  
    8|     "role" : "dbAdmin"  
    9|   } ],  
    10|   "roleName" : "test"  
    11| }, {  
    12|   "actions" : [ {  
    13|     "action" : "LIST_SESSIONS",  
    14|     "resources" : [ {  
    15|       "cluster" : true  
    16|     } ]  
    17|   }, {  
    18|     "action" : "KILL_ANY_SESSION",  
    19|     "resources" : [ {  
    20|       "cluster" : true  
    21|     } ]  
    22|   }, {  
    23|     "action" : "USE_UUID",  
    24|     "resources" : [ {  
    25|       "cluster" : true  
    26|     } ]  
    27|   }, {  
    28|     "action" : "COLL_STATS",  
    29|     "resources" : [ {  
    30|       "collection" : "",  
    31|       "db" : "staging"  
    32|     } ]  
    33|   } ],  
    34|   "inheritedRoles" : [ {  
    35|     "db" : "admin",  
    36|     "role" : "enableSharding"  
    37|   }, {  
    38|     "db" : "admin",  
    39|     "role" : "backup"  
    40|   } ],  
    41|   "roleName" : "ShardingAdmin"  
    42| }, {  
    43|   "actions" : [ {  
    44|     "action" : "CONN_POOL_STATS",  
    45|     "resources" : [ {  
    46|       "cluster" : true  
    47|     } ]  
    48|   }, {  
    49|     "action" : "CURSOR_INFO",  
    50|     "resources" : [ {  
    51|       "cluster" : true  
    52|     } ]  
    53|   }, {  
    54|     "action" : "LIST_DATABASES",  
    55|     "resources" : [ {  
    56|       "cluster" : true  
    57|     } ]  
    58|   }, {  
    59|     "action" : "SERVER_STATUS",  
    60|     "resources" : [ {  
    61|       "cluster" : true  
    62|     } ]  
    63|   }, {  
    64|     "action" : "TOP",  
    65|     "resources" : [ {  
    66|       "cluster" : true  
    67|     } ]  
    68|   }, {  
    69|     "action" : "LIST_SESSIONS",  
    70|     "resources" : [ {  
    71|       "cluster" : true  
    72|     } ]  
    73|   }, {  
    74|     "action" : "KILL_ANY_SESSION",  
    75|     "resources" : [ {  
    76|       "cluster" : true  
    77|     } ]  
    78|   } ],  
    79|   "inheritedRoles" : [ ],  
    80|   "roleName" : "SessionMonitor"  
    81| } ]  
  
What is MongoDB Atlas? →

