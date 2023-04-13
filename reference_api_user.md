Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Users

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The `users` resource allows you to create new Atlas users and assign them to
any Atlas project for which you have the `Project Owner` role.

You can also modify your own Atlas profile. If you are the owner of an Atlas
organization or project, you can also update the user roles for any user with
membership in that organization or project.

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

/users/{USER-ID}

|

Retrieves the profile for the specified Atlas user identified with the unique
identifier `{USER-ID}`.  
  
`GET`

|

/users/byName/{USER-NAME}

|

Retrieves the profile for the specified Atlas user with username `{USER-
NAME}`.  
  
`POST`

|

/users/

|

Creates a Atlas user and assigns it to one or more of your Atlas organizations
or projects.  
  
`PATCH`

|

/users/{USER-ID}

|

Updates the roles assigned to one Atlas user.  
  
What is MongoDB Atlas? →

