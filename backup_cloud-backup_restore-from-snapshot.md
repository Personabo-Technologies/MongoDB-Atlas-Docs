Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Restore from a Scheduled or On-Demand Snapshot

Share Feedback

On this page

  * Restore Considerations
  * Sharded Clusters
  * M2/M5 Clusters
  * Serverless Instances
  * Fallback Snapshots
  * Procedure
  * Restore a Cluster
  * Restore a Serverless Instance

Atlas lets you restore data from a scheduled or on-demand Cloud Backup. The
following sections describe restoring from a snapshot _without_ Encryption at
Rest using Customer Key Management. To restore from a snapshot using
Encryption at Rest using Customer Key Management, see Restore from a Snapshot
Using Encryption at Rest.

## Restore Considerations

In addition to the prerequisites applying to all restore procedures, be aware
of the following requirements and limitations when restoring from a scheduled
or on-demand Cloud Backup.

  * You must have the `Project Owner` role for the Atlas projects that contain the source and target database deployments to restore data from one Atlas database deployment to another.

  * If the `DefaultRWConcern` value on the source snapshot differs from the `DefaultRWConcern` value on the target database deployment, Atlas overrides the value on the source snapshot with the value on the target database deployment. If there is no value configured for the `DefaultRWConcern` on the target database deployment, Atlas keeps the value of `DefaultRWConcern` from the snapshot without explicit configuration. This may differ from the default value for that MongoDB version.

  * This feature is not available for `M0` clusters.

  * Atlas can restore Atlas Search indexes from a Cloud Backup snapshot only if both of the following are true:

    * You restore the Cloud Backup snapshot to the same cluster as the source of the backup.

    * The Atlas Search index exists in the cluster at the time of restoration. If you delete the Atlas Search index after the snapshot but before the restoration, Atlas can't restore the Atlas Search index from the snapshot.

Otherwise, you must manually rebuild Atlas Search indexes on the cluster.

### Sharded Clusters

  * If you are restoring a sharded cluster, the source and target clusters must have the same number of shards.

  * Atlas can't restore a sharded cluster snapshot to a replica set.

### M2/M5 Clusters

  * Starting with MongoDB 5.0, you can restore snapshots of clusters that run only the two most recent major versions of MongoDB to `M2` and `M5` clusters.

## Example

    * You can restore snapshots taken from clusters that run MongoDB 4.2 to an `M2` or `M5` cluster that runs MongoDB 5.0.

    * You can't restore snapshots taken from clusters that run MongoDB 4.0 to an `M2` or `M5` cluster that runs MongoDB 5.0.

### Serverless Instances

  * Atlas can't restore snapshots from shared clusters, dedicated clusters, or Cloud Manager to a serverless instance.

  * If you are restoring from a serverless instance, you can only restore the two most recent snapshots.

## Fallback Snapshots

If a scheduled snapshot fails for any reason, Atlas attempts to repeat the
snapshot process. If necessary, you may use the resulting fallback snapshot to
restore the cluster. This isn't recommended: fallback snapshots use a
different process from regular snapshots. They may contain inconsistent data.

Fallback snapshots are marked in the UI with a warning icon, and a warning
message appears in the restore modal window if the restore uses a fallback
snapshot.

## Warning

Restoring your cluster from a fallback snapshot may result in inconsistent
data across your cluster, and should be considered an option of last resort.

## Procedure

## Important

Atlas deletes all existing data on the target database deployment prior to the
restore. The cluster will be **unavailable** for the duration of the restore.

Atlas CLI

Atlas UI

### Restore a Cluster

To start a restore job for your project and cluster using the Atlas CLI, run
the following command:

    
    
    atlas backups restores start <automated|download|pointInTime> [options]  
      
  
To watch for a specific restore job to complete using the Atlas CLI, run the
following command:

    
    
    atlas backups restores watch <restoreJobId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas backups restores start and atlas backups
restores watch.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Restore a Serverless Instance

To start a restore job for your serverless instance using the Atlas CLI, run
the following command:

    
    
    atlas serverless backups restores create [options]  
      
  
To watch the specified backup restore job until it completes using the Atlas
CLI, run the following command:

    
    
    atlas serverless backups restores watch [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas serverless backups restores create and
atlas serverless backups restores watch.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Restore Your Database DeploymentRestore from Continuous Cloud Backup →

