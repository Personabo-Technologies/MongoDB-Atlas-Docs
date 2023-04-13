Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Legacy Backup Checkpoints

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

This resource allows you to view checkpoint metadata. Checkpoints are
additional restore points for sharded clusters at points in time between
regular snapshots. With checkpoints enabled, Atlas creates checkpoints at
configurable intervals of every 15, 30, or 60 minutes between snapshots.

## Important

### Legacy Backups Only

This resource only applies to clusters using Legacy Backups (Deprecated).

To create a checkpoint, Atlas stops the balancer and inserts a token into the
oplog of each shard and config server in the cluster. These checkpoint tokens
are lightweight and do not have a significant impact on performance or disk
use.

Restoring from a checkpoint requires Atlas to apply the oplog of each shard
and config server to the last snapshot captured before the checkpoint.
Restoration from a checkpoint takes longer than restoration from a snapshot.

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
GET

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backupCheckpoints

|

Retrieve all checkpoints for the specified sharded cluster.  
  
GET

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backupCheckpoints/{CHECKPOINT-ID}

|

Retrieve one checkpoint for the specified sharded cluster.  
  
What is MongoDB Atlas? →

