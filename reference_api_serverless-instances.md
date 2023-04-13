Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Serverless Instances

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `serverless` resource provides access to your serverless instance
configurations. The resource lets you create, edit and delete serverless
instances. The resource requires your Project ID.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{groupId}/serverless/{instanceName}

|

Returns one serverless instance in the specified project.  
  
`GET`

|

/groups/{groupId}/serverless

|

Returns all serverless instances in the specified project.  
  
`POST`

|

/groups/{groupId}/serverless

|

Creates one serverless instance in the specified project.  
  
`PATCH`

|

/groups/{groupId}/serverless/{instanceName}

|

Updates one serverless instance in the specified project.  
  
`DELETE`

|

/groups/{groupId}/serverless/{instanceName}

|

Removes one serverless instance in the specified project.  
  
What is MongoDB Atlas? →

