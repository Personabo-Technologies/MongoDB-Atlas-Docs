Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Cloud Backup Schedule

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

### Applies to Scheduled Cloud Backups Only

This resource applies to:

  * Clusters using Back Up Your Database Deployment and

  * Scheduled snapshots, not on-demand snapshots.

The `/backup/schedule` resource enables you to view and modify the snapshot
scheduling and retention settings for an Atlas cluster with Back Up Your
Database Deployment enabled.

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

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/schedule

|

Get the current snapshot schedule and retention settings for the cluster with
`{CLUSTER-NAME}`.  
  
`PATCH`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/schedule

|

Modify the snapshot schedule or retention settings for the cluster with
`{CLUSTER-NAME}`.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/schedule

|

Delete all the snapshot schedules for the cluster with `{CLUSTER-NAME}`.  
  
What is MongoDB Atlas? →

