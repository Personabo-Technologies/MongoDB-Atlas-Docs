Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Restore Legacy Backup Jobs

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

Create and retrieve restores jobs for a MongoDB cluster. A restore job
restores a MongoDB cluster to its state from an existing snapshot.

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
  
GET

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restoreJobs

|

Retrieve all restore jobs for the specified cluster.  
  
GET

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restoreJobs/{JOB-ID}

|

Retrieve one restore job for the specified cluster.  
  
POST

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restoreJobs

|

Create one restore job for the specified cluster.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists  
  
What is MongoDB Atlas? →

