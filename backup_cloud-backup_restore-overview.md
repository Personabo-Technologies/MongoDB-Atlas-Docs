Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Restore Your Database Deployment

Share Feedback

On this page

  * Prerequisites
  * Stop Client Operations during Restoration
  * View Status of Snapshot Restorations
  * View Cluster Restore Jobs
  * View Serverless Instance Restore Jobs

Atlas lets you restore data from

  * scheduled and on-demand snapshots

  * continuous cloud backup

  * locally-downloaded snapshot files

  * snapshots of a cluster using Encryption at Rest using Customer Key Management

## Tip

### See also:

  * To learn more about Cloud Backup, see Back Up Your Database Deployment.

  * To learn how to restore data from a legacy backup snapshot, see Restore a Cluster from a Legacy Backup Snapshot.

## Prerequisites

### Stop Client Operations during Restoration

You must ensure that the target Atlas database deployment doesn't receive
client requests during restoration. You can restore to a new database
deployment and reconfigure your application to use that new database
deployment once it is running for maximum uptime.

## View Status of Snapshot Restorations

Atlas CLI

Atlas UI

### View Cluster Restore Jobs

To list all cloud backup restore jobs for your database deployment using the
Atlas CLI, run the following command:

    
    
    atlas backups restores describe <restoreJobId> [options]  
      
  
To return the details for the cloud backup restore job you specify using the
Atlas CLI, run the following command:

    
    
    atlas accessLists create [entry] [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas backups restores describe and atlas
accessLists create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### View Serverless Instance Restore Jobs

To return all cloud backup restore jobs for the specified serverless instance
in your project using the Atlas CLI, run the following command:

    
    
    atlas serverless backups restores describe [options]  
      
  
To describe a cloud backup restore job using the Atlas CLI, run the following
command:

    
    
    atlas accessLists create [entry] [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas serverless backups restores describe and
atlas accessLists create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Export Cloud Backup SnapshotRestore from a Scheduled or On-Demand Snapshot →

