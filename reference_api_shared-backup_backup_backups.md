Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Shared-Tier Snapshots

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Note

This resource applies only to `M2` and `M5` shared clusters.

The `/backup/tenant/snapshots` resource enables you to view and download `M2`
and `M5` cluster snapshots.

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

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/snapshots

|

Get all snapshots for the specified `M2` or `M5` cluster.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/snapshots/{SNAPSHOT-
ID}

|

Get the snapshot associated with `{SNAPSHOT-ID}`.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/download

|

Request to download a specified snapshot.  
  
What is MongoDB Atlas? →

