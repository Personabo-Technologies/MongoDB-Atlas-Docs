Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Restore from Continuous Cloud Backup

Share Feedback

On this page

  * Restore Considerations
  * Procedure
  * Restore a Cluster
  * Restore a Serverless Instance

Atlas lets you restore data from a Continuous Cloud Backup by specifying one
of the following options:

  * A specific date and time to which you want to restore

  * A specific oplog entry from which you want to restore

## Restore Considerations

  * You must have the `Project Owner` role for the Atlas projects that contain the source and target database deployments to restore data from one Atlas database deployment to another.

  * If the `DefaultRWConcern` value on the source snapshot differs from the `DefaultRWConcern` value on the target database deployment, Atlas overrides the value on the source snapshot with the value on the target database deployment. If there is no value configured for the `DefaultRWConcern` on the target database deployment, Atlas keeps the value of `DefaultRWConcern` from the snapshot without explicit configuration. This may differ from the default value for that MongoDB version.

  * This feature is only available for `M10+` dedicated clusters and serverless instances.

  * If you are restoring from Serverless Continuous Backup, you can only use a Date & Time within the last 72 hours. Serverless instances don't support restoring from an oplog entry.

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

After the restore completes, Atlas takes a snapshot of the restored cluster.
This snapshot has a retention period equal to the cluster's continuous cloud
backup window.

← Restore from a Scheduled or On-Demand SnapshotRestore from a Locally-
Downloaded Snapshot →

