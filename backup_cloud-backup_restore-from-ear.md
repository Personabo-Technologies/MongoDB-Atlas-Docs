Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Restore from a Snapshot Using Encryption at Rest

Share Feedback

On this page

  * Restore Restrictions
  * Procedure
  * Troubleshooting Encryption at Rest

Atlas lets you restore data from a snapshot of a cluster using Encryption at
Rest using Customer Key Management

## Restore Restrictions

  * You must have the `Project Owner` role for the Atlas projects that contain the source and target database deployments to restore data from one Atlas database deployment to another.

  * If the `DefaultRWConcern` value on the source snapshot differs from the `DefaultRWConcern` value on the target database deployment, Atlas overrides the value on the source snapshot with the value on the target database deployment. If there is no value configured for the `DefaultRWConcern` on the target database deployment, Atlas keeps the value of `DefaultRWConcern` from the snapshot without explicit configuration. This may differ from the default value for that MongoDB version.

  * This feature is only available for `M10+` dedicated clusters.

  * Atlas can only restore to a cluster that uses the same encryption provider as the source cluster. Snapshots taken from clusters without Encryption at Rest using Customer Key Management cannot be restored to a cluster with it, or to a Cloud Manager project.

## Procedure

## Important

Atlas deletes all existing data on the target database deployment prior to the
restore. The cluster will be **unavailable** for the duration of the restore.

## Important

If the target project doesn't have a cluster with Encryption at Rest enabled,
you can either deploy a cluster with Encryption at Rest, or enable Encryption
at Rest in an existing cluster.

Clusters that use AWS KMS encrypt their PIT restore oplog data with the
customer's CMK. The current CMK must be valid for the encrypted oplog data to
perform a restore from a snapshot.

  1. Click Database in the top-left corner of Atlas.

  2. From the Database Deployments view, click on the cluster name.

  3. Click the Backup tab.

If the cluster has no Backup tab, then Atlas backups are disabled for that
cluster and no snapshots are available. You can enable backups when modifying
the cluster.

  4. Click Restore in the Actions column for the snapshot you want to restore.

  5. From the Restore dialog, select the target Atlas Project to which you want to restore. You can restore to any Atlas project for which the authenticated Atlas user has the `Project Owner` role.

  6. Select the Cluster to restore to. You can only restore to an Atlas replica set running Encryption at Rest. The target cluster must run the same or greater version of MongoDB as the MongoDB Version of the snapshot.

After the restoration procedure, Atlas triggers a key rotation for MongoDB
encryption key. Atlas then encrypts the new MongoDB encryption keys based on
the configured Encryption at Rest provider for the target cluster.

  7. Restart your application and ensure it uses the new target cluster.

### Troubleshooting Encryption at Rest

If Atlas has an issue with the encryption of either the snapshot or the target
cluster, it displays one of the following errors:

Error

|

Result  
  
|  
  
Cannot restore a non-encrypted snapshot to a cluster with Encryption at Rest
enabled.

|

The snapshot cannot be restored to Atlas.  
  
Target cluster does not have encryption enabled.

|

You can either deploy a new target cluster with Encryption at Rest, or enable
Encryption at Rest on your desired target cluster.  
  
Encryption provider of target cluster does not match selected snapshot's
encryption provider.

|

The encryption provider for the snapshot and target cluster do not match. You
can either:

  1. Create a new snapshot with the same encryption provider.

  2. Change the encryption provider for the target cluster.

  
  
Encryption credentials on snapshot are not present.

|

Atlas cannot restore a snapshot whose encryption key was deleted.  
  
← Restore from a Locally-Downloaded SnapshotImport Archive from S3 →

