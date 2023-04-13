Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Live Migration (Push)

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Considerations

  * Source organizations, projects, and MongoDB clusters reside on Cloud Manager or Ops Manager.

  * Destination organizations, projects, and MongoDB clusters reside on Atlas.

  * Source databases can't use any authentication except SCRAM-SHA.

## Endpoints

`https://cloud.mongodb.com/api/atlas/v1.0`

Method

|

Endpoint

|

Description  
  
||  
  
`POST`

|

/orgs/{orgId}/liveMigrations/linkTokens

|

Create one new link-token for push live migrations.  
  
`DELETE`

|

/orgs/{orgId}/liveMigrations/linkTokens

|

Delete one link-token.  
  
`POST`

|

/groups/{groupId}/liveMigrations/validate

|

Create one new validation request for push live migration.  
  
`GET`

|

/groups/{groupId}/liveMigrations/validate/{validationId}

|

Return status for one validation job for push live migration.  
  
`POST`

|

/groups/{groupId}/liveMigrations

|

Create one new push live migration job.  
  
`GET`

|

/groups/{groupId}/liveMigrations/{liveMigrationId}

|

Return status of one push live migration job and the list of configured
migration hosts.  
  
`PUT`

|

/groups/{groupId}/liveMigrations/{liveMigrationId}/cutover

|

Start one push live migration process.  
  
What is MongoDB Atlas? →

