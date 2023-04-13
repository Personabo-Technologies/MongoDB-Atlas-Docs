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

You can delete an AWS private endpoint for the Data Federations in the project
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
private endpoint.

## Resources

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    DELETE /groups/{GROUP-ID}/privateNetworkSettings/endpointIds/{ENDPOINT-ID}  
      
  
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
Atlas Data Federation supports AWS private endpoints using the AWS PrivateLink
feature.  
  
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

