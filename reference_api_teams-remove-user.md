Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Remove a User from a Team

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

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    DELETE /orgs/{ORG-ID}/teams/{TEAM-ID}/users/{USER-ID}  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`ORG-ID`

|

Required.

|

The unique identifier for the organization that contains the team from which
you want to remove a database user.  
  
`TEAM-ID`

|

Required

|

The unique identifier of the team from which you want to remove a database
user.  
  
`USER-ID`

|

Required

|

The unique identifier for the database user that you want to remove from the
specified team.  
  
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

This endpoint does not use HTTP request path parameters.

## Response

This endpoint does not return a response body.

## Example

### Request

    
    
    curl -X DELETE -i --digest --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
      
     "https://cloud.mongodb.com/api/atlas/v1.0/orgs/6001f2c580eef55aedbc6bb1/teams/6bdb97c780eef5147f823666/users/69g63c0980eef52994dbfcge"  
  
### Response

This endpoint doesn't return a response body.

What is MongoDB Atlas? →

