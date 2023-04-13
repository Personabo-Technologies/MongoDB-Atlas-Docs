Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Custom Role

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

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

The Atlas Administration API uses HTTP Digest Authentication. Provide your
Atlas username as the username and Atlas Administration API key as the
password as part of the HTTP request.

This endpoint requires that the Atlas user has the `Owner` role. To view the
available Atlas users, click on Users & Teams in the left-hand navigation.

For complete documentation on configuring API access for an Atlas project, see
Get Started with the Atlas Administration API.

## Syntax

    
    
    POST /groups/{GROUP-ID}/customDBRoles/roles  
      
  
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

## Note

This value should be `admin` for all roles except read and readWrite.  
  
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

## Important

The specified role name can only contain letters, digits, underscores, and
dashes. Additionally, you cannot specify a role name which meets any of the
following criteria:

  * Is a name already used by an existing custom role in the project

  * Is a name of any of the built-in roles

  * Is `atlasAdmin`

  * Starts with `xgen-`

  
  
### Response Elements

This endpoint does not have response elements.

## Example Request

### Request

## Important

You must modify the following code block with the appropriate credentials and
project ID.

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
     --header 'Content-Type: application/json' \  
     --include \  
     --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/customDBRoles/roles" --data '  
     {  
       "actions" : [ {  
         "action" : "CONN_POOL_STATS",  
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
    }'  
  
### Response

    
    
    HTTP/1.1 202 Accepted  
      
      
    {  
      "actions" : [ {  
        "action" : "CONN_POOL_STATS",  
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

