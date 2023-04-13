Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Custom Roles

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `customDBRoles` resource lets you retrieve, create, and change custom
roles in your cluster. Use custom roles to specify custom sets of actions that
the Atlas built-in roles can't describe.

The following statements describe custom roles:

  * You define custom roles at the project level, for all clusters in the project.

  * The `customDBRoles` resource supports a subset of MongoDB privilege actions. For a complete list of privilege actions available for this resource, see Custom Role actions.

  * Using the Atlas Administration API, you can create a subset of custom role actions. To create a wider list of custom role actions, use the Atlas user interface.

  * Custom roles must include actions that all project's clusters support, and that are compatible with each MongoDB version used by your project's clusters. For example, if your project has MongoDB 4.2 clusters, you can't create custom roles that use actions introduced in MongoDB 4.4.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/customDBRoles/roles

|

Get all custom roles in the project.  
  
`GET`

|

/groups/{GROUP-ID}/customDBRoles/roles/{ROLE-NAME}

|

Get the custom role named {ROLE-NAME}.  
  
`POST`

|

/groups/{GROUP-ID}/customDBRoles/roles

|

Create a new custom role in the project.  
  
`PATCH`

|

/groups/{GROUP-ID}/customDBRoles/roles/{ROLE-NAME}

|

Update a custom role in the project.  
  
`DELETE`

|

/groups/{GROUP-ID}/customDBRoles/roles/{ROLE-NAME}

|

Delete a custom role from the project.  
  
What is MongoDB Atlas? →

