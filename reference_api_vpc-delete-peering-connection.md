Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete One Existing Network Peering Connection

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

Delete one network peering connection associated with one Atlas project. You
must have the `Project Owner` role or the `Organization Owner` role to
successfully call this endpoint.

## Important

### AWS Only

If you delete the last network peering connection associated with a project,
Atlas also removes any AWS security groups from the project IP access list.

## Resource

    
    
    DELETE /groups/{GROUP-ID}/peers/{PEER-ID}  
      
  
### Request Path Parameters

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`GROUP-ID`

|

string

|

Required

|

Unique identifier for the project.  
  
`PEER-ID`

|

string

|

Required

|

Atlas assigned unique ID for the peering connection.

## Note

This is separate from the peering container ID. Use the Get All Peering
Connections API to retrieve a list of peering connection ids for an Atlas
project.  
  
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

This endpoint doesn't use HTTP request body parameters.

## Response Elements

This endpoint does not have response elements.

## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|   --header "Accept: application/json" \  
    3|   --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794dee37132bb7b/peers/1112222b3bf99403840e8934?pretty=true"  
  
## Example Response

This endpoint returns an empty JSON object.

What is MongoDB Atlas? →

