Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Private Endpoints

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Resources

`https://cloud.mongodb.com/api/atlas/v1.0`

The following lists the endpoints available for managing private endpoints on
AWS, Azure, and Google Cloud:

Method

|

Endpoint

|

Description  
  
||  
  
GET

|

/groups/{GROUP-ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService

|

Retrieve details for all private endpoint services for AWS, Azure, or Google
Cloud in one Atlas project.  
  
GET

|

/groups/{GROUP-ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService/{ENDPOINT-
SERVICE-ID}

|

Retrieve details for one private endpoint service for AWS, Azure, or Google
Cloud in an Atlas project.  
  
POST

|

/groups/{GROUP-ID}/privateEndpoint/endpointService/

|

Create one private endpoint service for AWS, Azure, or Google Cloud in an
Atlas project.  
  
DELETE

|

/groups/{GROUP-ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService/{ENDPOINT-
SERVICE-ID}

|

Delete one private endpoint service for AWS, Azure, or Google Cloud in an
Atlas project.  
  
GET

|

/groups/{GROUP-ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService/{ENDPOINT-
SERVICE-ID}/endpoint/{ENDPOINT-ID}

|

Retrieve details for one private endpoint for AWS or Azure in an Atlas
project.  
  
POST

|

/groups/{GROUP-ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService/{ENDPOINT-
SERVICE-ID}/endpoint

|

Create one private endpoint or endpoint group for AWS, Azure, or Google Cloud
in an Atlas project.  
  
DELETE

|

/groups/{GROUP-ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService/{ENDPOINT-
SERVICE-ID}/endpoint/{ENDPOINT-ID}

|

Delete one private endpoint or endpoint group for AWS, Azure, or Google Cloud
from an Atlas project.  
  
GET

|

/groups/{GROUP-ID}/privateEndpoint/regionalMode

|

Retrieve whether the regionalized private endpoint feature is enabled for one
Atlas project.  
  
PATCH

|

/groups/{GROUP-ID}/privateEndpoint/regionalMode

|

Enable or disable the regionalized private endpoint feature for one Atlas
project.  
  
What is MongoDB Atlas? →

