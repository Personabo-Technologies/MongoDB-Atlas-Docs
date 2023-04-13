Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Serverless Private Endpoints

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

The following lists the endpoints available for managing private endpoints for
serverless instances:

Method

|

Endpoint

|

Description  
  
||  
  
GET

|

/groups/{GROUP-ID}/privateEndpoint/serverless/instance/ {INSTANCE-
NAME}/endpoint

|

Returns all private endpoints for one Atlas serverless instance.  
  
GET

|

/groups/{GROUP-ID}/privateEndpoint/serverless/instance/ {INSTANCE-
NAME}/endpoint/{ENDPOINT-ID}

|

Returns one private endpoint for one Atlas serverless instance.  
  
POST

|

/groups/{GROUP-ID}/privateEndpoint/serverless/instance/ {INSTANCE-
NAME}/endpoint

|

Creates one private endpoint for one Atlas serverless instance.  
  
DELETE

|

/groups/{GROUP-ID}/privateEndpoint/serverless/instance/ {INSTANCE-
NAME}/endpoint/{ENDPOINT-ID}

|

Deletes one private endpoint for one Atlas serverless instance.  
  
PATCH

|

/groups/{GROUP-ID}/privateEndpoint/serverless/instance/ {INSTANCE-
NAME}/endpoint/{ENDPOINT-ID}

|

Updates one private endpoint for one Atlas serverless instance.  
  
What is MongoDB Atlas? →

