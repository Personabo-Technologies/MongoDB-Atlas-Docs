Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Teams

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `teams` resource provides access to retrieve or create Atlas teams.

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

/orgs/{ORG-ID}/teams

|

Get all teams in an organization associated with `{ORG-ID}` to which the
authenticated user has access.  
  
`GET`

|

/orgs/{ORG-ID}/teams/{TEAM-ID}

|

Get the team with ID `{TEAM-ID}` in the organization associated with `{ORG-
ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/teams/byName/{TEAM-NAME}

|

Get the team with name `{TEAM-NAME}` in the organization associated with
`{ORG-ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/teams/{TEAM-ID}/users

|

Get all users assigned to the team with ID `{TEAM-ID}` in the organization
associated with `{ORG-ID}`.  
  
`POST`

|

/orgs/{ORG-ID}/teams

|

Create one team in the organization associated with `{ORG-ID}}`.  
  
`POST`

|

/orgs/{ORG-ID}/teams/{TEAM-ID}/users

|

Add one user from the organization associated with `{ORG-ID}` to the team with
ID `{TEAM-ID}`.  
  
`POST`

|

/{GROUP-ID}/teams/

|

Assign one Atlas team to the project associated with `{GROUP-ID}`.  
  
`PATCH`

|

/orgs/{ORG-ID}/teams/{TEAM-ID}

|

Rename one team in one Atlas organization.  
  
`PATCH`

|

/groups/{GROUP-ID}/teams/{TEAM-ID}

|

Update the roles of one team in one Atlas project.  
  
`DELETE`

|

/orgs/{ORG-ID}/teams/{TEAM-ID}/users/{USER-ID}

|

Remove the specified user from the specified team.  
  
`DELETE`

|

/groups/{GROUP-ID}/teams/{TEAM-ID}

|

Removes the specified team from the specified project.  
  
`DELETE`

|

/orgs/{ORG-ID}/teams/{TEAM-ID}

|

Delete the team with ID `{TEAM-ID}` from the organization specified to `{ORG-
ID}`.  
  
## Note

The API endpoints to Add Teams to a Project and Get Teams Assigned to a
Project are documented in the Projects section.

What is MongoDB Atlas? →

