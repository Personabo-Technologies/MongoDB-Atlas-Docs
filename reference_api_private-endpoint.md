Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Private Endpoints (Deprecated)

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Required Roles

You must have one of the following roles to successfully call these resources:

  * `Organization Owner`

  * `Project Owner`

## Resources

`https://cloud.mongodb.com/api/atlas/v1.0`

The following lists the endpoints available for managing Private Endpoints.

Method

|

Endpoint

|

Description  
  
||  
  
GET

|

/groups/{GROUP-ID}/privateEndpoint

|

Retrieve details for all private endpoint connections in an Atlas project.  
  
POST

|

/groups/{GROUP-ID}/privateEndpoint

|

Create one private endpoint connection in an Atlas project.  
  
GET

|

/groups/{GROUP-ID}/privateEndpoint/{privateLinkId}

|

Retrieve details for one private endpoint connection by ID in an Atlas
project.  
  
DELETE

|

/groups/{GROUP-ID}/privateEndpoint/{privateLinkId}

|

Remove one private endpoint connection in an Atlas project.  
  
POST

|

/groups/{GROUP-ID}/privateEndpoint/{privateLinkId}/interfaceEndpoints

|

Add one interface endpoint to a private endpoint connection in an Atlas
project.  
  
GET

|

/groups/{GROUP-
ID}/privateEndpoint/{privateLinkId}/interfaceEndpoints/{interfaceEndpointId}

|

Retrieve one interface endpoint in a private endpoint connection in an Atlas
project.  
  
DELETE

|

/groups/{GROUP-
ID}/privateEndpoint/{privateLinkId}/interfaceEndpoints/{interfaceEndpointId}

|

Remove one interface endpoint from a private endpoint connection in an Atlas
project.  
  
What is MongoDB Atlas? →

