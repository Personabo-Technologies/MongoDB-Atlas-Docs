Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Serverless Instance Backups

Share Feedback

On this page

  * Limitations
  * View Serverless Instance Snapshots

Atlas takes snapshots of serverless instances using the native snapshot
capabilities of the serverless instances's cloud service provider.

## Important

You can't disable backup of serverless instances.

Atlas offers the following backup options for serverless instances:

Option

|

Description  
  
|  
  
Serverless Continuous Backup

|

Atlas takes incremental snapshots of the data in your serverless instance
every six hours and lets you restore the data from a selected point in time
within the last 72 hours. Atlas also takes daily snapshots and retains these
daily snapshots for 35 days. To learn more, see Serverless Instance Costs.  
  
Basic Backup

|

Atlas takes incremental snapshots of the data in your serverless instance
every six hours and retains only the two most recent snapshots. You can use
this option for free.  
  
To learn more, see Configure Serverless Instance Backup.

## Limitations

  * You can't download serverless instance snapshots.

  * Custom policies are not supported for serverless instance snapshots. Atlas always takes snapshots every six hours.

If you require finer-grained backups, consider migrating to a dedicated
cluster.

  * Atlas doesn't support on-demand snapshots for serverless instances.

  * You can't restore snapshots from shared clusters, dedicated clusters, or from Cloud Manager to serverless instances.

## View Serverless Instance Snapshots

Atlas displays existing snapshots on the Snapshots page.

To view your snapshots:

Atlas CLI

Atlas UI

### View Snapshots

To return all cloud backup snapshots for the specified serverless instance in
your project using the Atlas CLI, run the following command:

    
    
    atlas serverless backups snapshots list <clusterName> [options]  
      
  
To return the details for the specified snapshot for your project using the
Atlas CLI, run the following command:

    
    
    atlas serverless backups snapshots describe [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas serverless backups snapshots list and
atlas serverless backups snapshots describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### View Snapshot Status

To watch the specified snapshot in your project until it reaches a completed
or failed status using the Atlas CLI, run the following command:

    
    
    atlas serverless backups snapshots watch [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas serverless backups snapshots watch.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Shared Cluster BackupsBackup Scheduling, Retention, and On-Demand Snapshots
→

