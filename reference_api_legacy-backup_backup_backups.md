Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Legacy Backup Snapshots

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Legacy Backup Deprecated

Effective 23 March 2020, all new clusters can _only_ use Cloud Backups.

When you upgrade to 4.2, your backup system upgrades to cloud backup if it is
currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The `snapshots` resource enables you to view snapshot metadata, edit snapshot
expiration dates, and remove existing snapshots. A snapshot is a backup of
your data captured at a specific point in time.

## Important

### Legacy Backups Only

This resource only applies to clusters using Legacy Backups (Deprecated).

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/snapshots

|

Get all snapshots for the specified cluster.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/snapshots/{SNAPSHOT-ID}

|

Get the specified snapshot for the cluster.  
  
`PATCH`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/snapshots/{SNAPSHOT-ID}

|

Change the expiration date for the specified snapshot.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/snapshots/{SNAPSHOT-ID}

|

Delete the specified snapshot.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists  
  
What is MongoDB Atlas? →

