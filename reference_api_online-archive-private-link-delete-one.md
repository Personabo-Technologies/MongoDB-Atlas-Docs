Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete One Private Endpoint

Share Feedback

On this page

  * Permissions Required
  * Resources
  * Syntax
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Examples
  * Request

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

You can delete an AWS private endpoint for the online archives in the project
from the API.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Permissions Required

You must have the `GROUP_ATLAS_ADMIN` (`Project Owner`) role to delete a
private endpoint for an online archive.

## Resources

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /groups/{GROUP-ID}/privateNetworkSettings/endpointIds/{ENDPOINT-ID}  
      
  
## Request Parameters

### Request Path Parameters

Path Element

|

Necessity

|

Description  
  
||  
  
`GROUP-ID`

|

Required

|

Unique 24-digit hexadecimal string that identifies the project.  
  
`ENDPOINT-ID`

|

Required

|

Unique 22-character alphanumeric string that identifies the private endpoint.
Atlas supports AWS private endpoints using the |aws| PrivateLink feature.  
  
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

## Response Elements

The HTTP response returns an empty JSON document.

## Examples

### Request

## Example

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
       --header "Accept: application/json" \  
       --header "Content-Type: application/json" \  
       --include \  
       --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateNetworkSettings/endpointIds/{ENDPOINT-ID}?pretty=true"  
  
What is MongoDB Atlas? →

