Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Cloud Provider Access

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The `cloudProviderAccess` resource allows you to register and authorize AWS
IAM roles in Atlas.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/cloudProviderAccess

|

Retrieve existing AWS IAM roles.  
  
`POST`

|

/cloudProviderAccess

|

Create an AWS IAM role.  
  
`PATCH`

|

/cloudProviderAccess/{ROLE-ID}

|

Authorize and configure an AWS Assumed IAM role.  
  
`DELETE`

|

/cloudProviderAccess/{ROLE-ID}

|

Deauthorize an AWS Assumed IAM role.  
  
What is MongoDB Atlas? →

