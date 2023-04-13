Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Projects

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The `groups` resource provides access to retrieve or create Atlas projects.

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

/groups

|

Get all projects that the authenticated user can access.  
  
`GET`

|

/groups/{GROUP-ID}

|

Get information about the project associated with `{GROUP-ID}`.  
  
`GET`

|

/groups/byName/{GROUP-NAME}

|

Get information about the project associated with `{GROUP-NAME}`.  
  
`POST`

|

/groups

|

Create one project.  
  
`DELETE`

|

/groups/{GROUP-ID}

|

Delete one project.  
  
`GET`

|

/groups/{GROUP-ID}/teams/

|

Get information about the teams assigned to the project associated with
`{GROUP-ID}`.  
  
`POST`

|

/groups/{GROUP-ID}/teams/

|

Assign an Atlas team to the project associated with `{GROUP-ID}`.  
  
`DELETE`

|

/groups/{GROUP-ID}/teams/{TEAM-ID}

|

Removes the specified Atlas team from the specified project.  
  
`GET`

|

/groups/{GROUP-ID}/users

|

Get information about the Atlas users assigned to the project associated with
`{GROUP-ID}`.  
  
`DELETE`

|

/groups/{GROUP-ID}/users/{USER-ID}

|

Remove the specified Atlas user from the project associated with `{GROUP-ID}`.  
  
`GET`

|

/groups/{GROUP-ID}/invites

|

Retrieves all pending invitations to the project associated with `{GROUP-ID}`.  
  
`PATCH`

|

/groups/{GROUP-ID}/invites

|

Update one pending invitation to the project associated with `{GROUP-ID}`.  
  
`GET`

|

/groups/{GROUP-ID}/invites/{INVITATION-ID}

|

Retrieves one pending invitation to a project associated with `{INVITATION-
ID}`.  
  
`POST`

|

/groups/{GROUP-ID}/invites

|

Invite one user to the project associated with `{GROUP-ID}`.  
  
`PATCH`

|

/groups/{GROUP-ID}/invites/{INVITATION-ID}

|

Update one pending invitation by `{INVITATION-ID}` to the project associated
with `{GROUP-ID}`.  
  
`DELETE`

|

/groups/{GROUP-ID}/invites/{INVITATION-ID}

|

Deletes one pending invitation to a project identified by `{INVITATION-ID}`.  
  
`GET`

|

/groups/{GROUP-ID}/settings

|

Retrieve information about the settings for the project identified by `{GROUP-
ID}`.  
  
`PATCH`

|

/groups/{GROUP-ID}/settings

|

Update the settings for the project identified by `{GROUP-ID}`.  
  
What is MongoDB Atlas? →

