Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete One Federated Database Instance

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
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

`https://cloud.mongodb.com/api/atlas/v1.0`

Use this endpoint to delete a specific federated database instance associated
with an Atlas project.

## Syntax

    
    
    DELETE /groups/{GROUP-ID}/dataFederation/{NAME}  
      
  
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

The unique identifier for the project.  
  
`NAME`

|

Require

|

The name of the federated database instance that you want to delete.

You can use the Get All Federated Database Instances endpoint to retrieve all
federated database instances associated with the project. The `name` field in
the response of that endpoint corresponds to the `NAME` parameter here.  
  
### Request Query Parameters

The following query parameters are optional:

Query Parameter

|

Type

|

Description

|

Default  
  
|||  
  
`pretty`

|

boolean

|

Displays response in a prettyprint format.

|

`false`  
  
`envelope`

|

boolean

|

Specifies whether or not to wrap the response in an envelope.

|

`false`  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

This endpoint returns an empty JSON document.

## Example

### Request

    
    
    curl -u "username:apiKey" --digest \  
      
     --header "Accept: application/json" \  
     --header "Content-Type: application/json" \  
     --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/dataFederation/{NAME}?pretty=true"  
  
### Response

    
    
    {}  
      
  
What is MongoDB Atlas? →

