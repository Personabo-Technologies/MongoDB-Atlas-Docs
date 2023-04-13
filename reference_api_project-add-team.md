Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Add Teams to a Project

Share Feedback

On this page

  * Syntax
  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example
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

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

Atlas limits the number of users to a maximum of 100 teams per project and a
maximum of 250 teams per organization.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /groups/{GROUP-ID}/teams  
      
  
## Request

### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required.

|

The unique identifier for the project to which you are adding the team or
teams.  
  
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

Specify an array of documents, where each document represents one team you
want to associate to the project. You must specify an array even if you are
only associating a single team to the project.

Name

|

Type

|

Description  
  
||  
  
`teamId`

|

string

|

The unique identifier of the team you want to associate with the project. You
must specify a `teamId` of an existing team, and your team and project must
share the same parent organization.

You can use the Get All Teams endpoint to obtain the list of `teamId`s in an
organization.  
  
`roleNames`

|

string array

|

Each string in the array represents a project role you want to assign to the
team. Every user associated with the team inherits these roles. You must
specify an array even if you are only associating a single role with the team.

The following are the valid roles and their associated mappings:

|

Role Names

|

Project Roles  
  
|  
  
`GROUP_OWNER`

|

`Project Owner`  
  
`GROUP_CLUSTER_MANAGER`

|

`Project Cluster Manager`  
  
`GROUP_DATA_ACCESS_ADMIN`

|

`Project Data Access Admin`  
  
`GROUP_DATA_ACCESS_READ_WRITE`

|

`Project Data Access Read/Write`  
  
`GROUP_DATA_ACCESS_READ_ONLY`

|

`Project Data Access Read Only`  
  
`GROUP_READ_ONLY`

|

`Project Read Only`  
  
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

Each element in the `result` array is one team assigned to the project.

Name

|

Type

|

Description  
  
||  
  
`links`

|

object array

|

This array includes one or more links to sub-resources and/or related
resources.

The relations between URLs are explained in the Web Linking Specification.  
  
`roleNames`

|

string array

|

Array of project roles assigned to the team.  
  
`teamId`

|

string

|

The unique identifier for the team.  
  
## Example

### Request

    
    
    curl -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
     --header "Accept: application/json" \  
     --header "Content-Type: application/json" \  
     --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/teams?pretty=true" \  
     --data '[ { "teamId" : "{TEAM-ID}", "roleNames" : [ "GROUP_OWNER" ] } ]'  
  
### Response

    
    
    {  
      
     "links": [  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/teams",  
             "rel": "self"  
         }  
     ],  
     "results": [  
         {  
             "links" : [  
               {  
                  "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/teams/{TEAM-ID}",  
                  "rel" : "self"  
               }  
             ],  
             "roleNames": [ "GROUP_OWNER" ],  
             "teamId": "{TEAM-ID}"  
         }  
     ],  
     "totalCount": 1  
    }  
  
What is MongoDB Atlas? →

