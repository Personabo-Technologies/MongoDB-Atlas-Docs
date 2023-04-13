Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Shared-Tier Restore Jobs

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

The `/backup/tenant/restores` resource enables you to view and create restore
jobs from `M2` and `M5` clusters.

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

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/restores

|

Get all restore jobs for the specified `M2` or `M5` cluster.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/restores/{RESTORE-ID}

|

Get the restore job associated to `{RESTORE-ID}`.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/restore

|

Create a new restore job from an `M2` or `M5` cluster snapshot to the
specified cluster.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists  
  
What is MongoDB Atlas? →

