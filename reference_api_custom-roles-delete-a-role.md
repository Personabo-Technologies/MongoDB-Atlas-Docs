Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete a Custom Role

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

## Important

You cannot delete a custom role in the following scenarios:

  * When deleting the role would leave one or more child roles with no parent roles or actions.

  * When deleting the role would leave one or more database users with no roles.

## Syntax

    
    
    DELETE /groups/{GROUP-ID}/customDBRoles/roles/{ROLE-NAME}  
      
  
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

The name of the role to update.  
  
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

This endpoint does not have response elements.

## Example Request

### Request

## Important

You must modify the following code block with the appropriate credentials and
project ID.

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
     --header 'Accept: application/json' \  
     --include \  
     --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/customDBRoles/roles/ShardingAdmin?pretty=true"  
  
### Response

This endpoint doesn't return a response body.

What is MongoDB Atlas? →

