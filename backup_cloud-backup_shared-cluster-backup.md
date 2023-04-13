Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Shared Cluster Backups

Share Feedback

On this page

  * Limitations
  * Backup Snapshot Storage Locations
  * View `M2`/`M5` Backup Snapshots

Atlas takes daily snapshots of `M2` and `M5` shared clusters. Atlas takes
these snapshots automatically starting 24 hours after you create your cluster.

## Note

You must have the `Project Owner` role for an Atlas project to manage backup
for the clusters in that project.

Atlas always takes `M2` and `M5` snapshots from a secondary node to minimize
performance impact.

Atlas retains the last 8 daily snapshots, which you can download or restore to
an Atlas cluster.

## Limitations

  * Custom policies are not supported for `M2` and `M5` cluster snapshots. Atlas always takes a single daily snapshot at the same time, starting 24 hours after the cluster was created.

If you require finer-grained backups, consider upgrading to an `M10` or larger
cluster tier.

  * On-demand snapshots are not supported for `M2` and `M5` clusters.

  * You can't restore `M2` and `M5` snapshots to a sharded cluster. You can only restore `M2` and `M5` snapshots to replica sets.

  * You can't restore serverless instance snapshots to `M2` and `M5` clusters.

  * Starting with MongoDB 5.0, you can restore snapshots of clusters that run only the two most recent major versions of MongoDB to `M2` and `M5` clusters.

## Example

    * You can restore snapshots taken from clusters that run MongoDB 4.4 to an `M2` or `M5` cluster that runs MongoDB 5.0.

    * You can't restore snapshots taken from clusters that run MongoDB version earlier than 4.4 to an `M2` or `M5` cluster that runs MongoDB 5.0.

## Backup Snapshot Storage Locations

The following table indicates where Atlas stores `M2` and `M5` cluster
snapshots:

Cluster Location

|

Snapshot Storage Location  
  
|  
  
Australia

|

Australia  
  
Germany

|

Germany  
  
Hong Kong

|

Australia  
  
India, Singapore, Taiwan

|

Asia  
  
USA

|

USA  
  
All other cluster locations

|

Ireland  
  
## View `M2`/`M5` Backup Snapshots

Atlas CLI

Atlas UI

To list cloud backup snapshots for your project and cluster using the Atlas
CLI, run the following command:

    
    
    atlas backups snapshots list <clusterName> [options]  
      
  
To return the details for the snapshot you specify using the Atlas CLI, run
the following command:

    
    
    atlas backups snapshots describe <snapshotId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas backups snapshot list and atlas backups
snapshots describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

Atlas displays existing snapshots in the All Daily Snapshots table. From this
table, you can restore or download your existing snapshots.

← Dedicated Cluster BackupsServerless Instance Backups →

