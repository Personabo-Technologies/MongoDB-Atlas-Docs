Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Encryption at Rest using Customer Key Management

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The following endpoints allow administrators to enable, disable, configure,
and retrieve the configuration for Encryption at Rest using Customer Key
Management.

## Note

Atlas encrypts all storage whether or not you use your own key management.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`PATCH`

|

/groups/{GROUP-ID}/encryptionAtRest

|

Enable, disable, and configure Encryption at Rest using Customer Key
Management for an Atlas project.  
  
`GET`

|

/groups/{GROUP-ID}/encryptionAtRest

|

Retrieve the current configuration for Encryption at Rest using Customer Key
Management for an Atlas project.  
  
What is MongoDB Atlas? →

