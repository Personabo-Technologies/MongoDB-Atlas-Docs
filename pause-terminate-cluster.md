Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Pause, Resume, or Terminate a Cluster

Share Feedback

On this page

  * Considerations for Paused Clusters
  * Pause One Cluster
  * Resume One Cluster
  * Terminate One Cluster

You can pause, resume, or terminate your clusters. For serverless instances,
see Terminate a Serverless Instance.

## Considerations for Paused Clusters

  * You can't:

    * Change the configuration of a paused cluster.

    * Read data from or write data to a paused cluster.

  * For paused clusters, Atlas:

    * Stops triggering configured alerts.

    * Stops all backups. Your existing snapshots remain until they expire.

  * If you have a Backup Compliance Policy enabled, when you resume a cluster, Atlas automatically enables Cloud Backup. If the Backup Compliance Policy has the Require Point in Time Restore to all clusters option set to On, Atlas automatically enables Continuous Cloud Backup and adjusts the restore window according to the Backup Compliance Policy. Atlas automatically modifies the backup to meet the minimum requirements of the Backup Compliance Policy.

  * If a paused cluster doesn't have Encryption at Rest enabled, you can't toggle the Require Encryption at Rest using Customer Key Management for all clusters option to On in a Backup Compliance Policy.

## Pause One Cluster

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

Depending on your cluster tier, Atlas either pauses clusters automatically or
when you manually initiate it.

### M0, M2, and M5 Clusters

Atlas automatically pauses all inactive `M0`, `M2`, and `M5` clusters after 60
days.

### M10+ Clusters

You can pause `M10` or larger clusters:

  * If they do not use NVMe storage.

  * For up to 30 days. If you don't resume the cluster within 30 days, Atlas resumes the cluster.

Atlas only charges paused clusters for storage. Atlas does not charge for any
other services or data transfer on paused clusters.

Atlas CLI

Atlas Administration API

Atlas UI

To pause a running Atlas cluster using the Atlas CLI, run the following
command:

    
    
    atlas clusters pause <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters pause.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### M0 Clusters

Atlas automatically stops collecting monitoring information for an `M0`
cluster after a few days of inactivity.

If there is no activity for 60 days, then Atlas automatically pauses the
cluster completely, disallowing any connections to it until you resume the
cluster. Atlas sends an email seven days before pausing the cluster. Atlas
sends another email after pausing the cluster.

You can resume or terminate an automatically paused cluster at any time. You
can't initiate a pause for `M0` clusters.

## Resume One Cluster

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

## Note

If you have a Backup Compliance Policy enabled, when you resume a cluster,
Atlas automatically enables Cloud Backup. If the Backup Compliance Policy has
the Require Point in Time Restore to all clusters option set to On, Atlas
automatically enables Continuous Cloud Backup and adjusts the restore window
according to the Backup Compliance Policy. Atlas automatically modifies the
backup to meet the minimum requirements of the Backup Compliance Policy.

To resume collection of monitoring information for an Atlas `M0` cluster
paused for monitoring, connect to that cluster using a MongoDB Driver,
`mongosh`, or Data Explorer.

To resume an Atlas `M0` cluster that Atlas paused due to inactivity, or an
Atlas `M10+` cluster that you paused previously:

Atlas CLI

Atlas UI

To start a paused Atlas cluster using the Atlas CLI, run the following
command:

    
    
    atlas clusters start <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters start.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Note

If you don't resume an `M10+` cluster within 30 days, Atlas resumes the
cluster.

## Terminate One Cluster

To terminate an Atlas cluster:

Atlas CLI

Atlas UI

## Note

If you enabled Termination Protection on your cluster, you must first disable
it.

To delete one cluster in the specified project using the Atlas CLI, run the
following command:

    
    
    atlas clusters delete <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

Atlas terminates the cluster after completing any in-progress deployment
changes.

Atlas bills for the hours that the cluster was active. To learn more about
Atlas billing, see Manage Billing.

## Warning

Terminating a cluster also deletes any backup snapshots for that cluster. See
Snapshot Schedule.

M10+

M0

## Note

### Public IP Address Retention

When you terminate a cluster with a lifetime of 12 hours or more, Atlas
reserves the cluster's public IP address, bound to its original cluster name.

The following time frames apply from the moment you terminate the cluster:

Cluster Lifetime

|

IP Address Retention  
  
|  
  
Less than 12 hours

|

Not retained  
  
12 to 35 hours

|

12 to 35 hours (equal to the cluster lifetime)  
  
36 hours or more

|

36 hours  
  
If, in the applicable time frame, you create a new cluster with the same name,
Atlas reassigns the reserved public IP address to that cluster.

Cluster IP addresses don't change when you or Atlas pause or resume clusters.

← Configure Maintenance WindowConfigure High Availability and Workload
Isolation →

