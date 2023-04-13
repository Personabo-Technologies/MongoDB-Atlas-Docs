Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get a Single Custom Role

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Examples
  * Request
  * Response

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

    
    
    GET /groups/{GROUP-ID}/customDBRoles/roles/{ROLE-NAME}  
      
  
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
  
`ROLE-NAME`

|

Required.

|

The name of the role to retrieve.  
  
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
  
## Examples

### Request

## Important

You must modify the following code block with the appropriate credentials and
project ID.

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
     --header 'Accept: application/json' \  
     --include \  
     --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/customDBRoles/roles/ShardingAdmin?pretty=true"  
  
### Response

    
    
    HTTP/1.1 200 OK  
      
      
    {  
      "actions" : [ {  
        "action" : "LIST_SESSIONS",  
        "resources" : [ {  
          "cluster" : true  
        } ]  
      }, {  
        "action" : "KILL_ANY_SESSION",  
        "resources" : [ {  
          "cluster" : true  
        } ]  
      }, {  
        "action" : "USE_UUID",  
        "resources" : [ {  
          "cluster" : true  
        } ]  
      }, {  
        "action" : "COLL_STATS",  
        "resources" : [ {  
          "collection" : "",  
          "db" : "staging"  
        } ]  
      } ],  
      "inheritedRoles" : [ {  
        "db" : "admin",  
        "role" : "enableSharding"  
      }, {  
        "db" : "admin",  
        "role" : "backup"  
      } ],  
      "roleName" : "ShardingAdmin"  
    }  
  
What is MongoDB Atlas? →

