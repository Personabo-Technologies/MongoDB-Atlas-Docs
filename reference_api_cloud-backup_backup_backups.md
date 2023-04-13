Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Cloud Backup

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Important

### Cloud Backups Only

This resource only applies to clusters using Back Up Your Database Deployment.

The `/backup/snapshots` resource enables you to view and delete Cloud Backups.

## Endpoints

`https://cloud.mongodb.com/api/atlas/v1.0`

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots

|

Get all Cloud Backups for the specified cluster.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots/{SNAPSHOT-ID}

|

Get the snapshot associated with `{SNAPSHOT-ID}`  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots/{SNAPSHOT-ID}

|

Delete the snapshot associated with `{SNAPSHOT-ID}`

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/snapshots

|

Take an on-demand snapshot.  
  
`GET`

|

/groups/{groupId}/serverless/{instanceName}/backup/snapshots/{snapshotId}

|

Return one snapshot of one serverless instance from the specified project.  
  
`GET`

|

/groups/{groupId}/serverless/{instanceName}/backup/snapshots

|

Return the last two snapshots of one serverless instance from the specified
project.  
  
What is MongoDB Atlas? →

