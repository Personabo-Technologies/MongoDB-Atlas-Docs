Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Recover a Point In Time with Continuous Cloud Backup

Share Feedback

On this page

  * Considerations
  * Procedure
  * Enable Continuous Cloud Backup.
  * Configure your continuous cloud backup restore window.
  * Recover a point in time with continuous cloud backup.

Continuous Cloud Backups replay the oplog to restore a cluster from a
particular point in time within a window specified in the Backup Policy. To
learn more, see Continuous Cloud Backups.

## Considerations

  * Enabling Continuous Cloud Backup increases the monthly cost of your cluster.

To learn more about the cost implications, see billing.

  * Atlas clusters where Continuous Cloud Backup is enabled store oplog data on AWS S3, including clusters backed by Azure and|gcp|.

  * If you disable Continuous Cloud Backup, Atlas will delete the continuous cloud backup history.

  * You can't configure a restore window that is longer than the Hourly Snapshot Retention Time.

  * If you select the Date & Time option, you can specify the time of restore with one minute of granularity.

  * If you select the Oplog Timestamp option, you can specify the time of restore with one second of granularity.

  * You can restore a cluster from any time during its continuous cloud backup window **except** between when you initiated a restore and when Atlas completes a snapshot after the restore.

  * Atlas might create a host rollback alert due to differences in the data between the source and target clusters. You can ignore this alert.

  * After the restore completes, Atlas takes a snapshot of the restored cluster. This snapshot has a retention period equal to the cluster's continuous cloud backup window.

## Procedure

The following process outlines the steps for setting up Continuous Cloud
Backup and recovering a point in time:

1

### Enable Continuous Cloud Backup.

  1. Create a new cluster, or click the __next to the name of your cluster and select Edit Configuration.

  2. Click Additional Settings.

  3. Toggle Turn on Cloud Backup to On.

  4. Toggle Continuous Cloud Backup to On.

2

### Configure your continuous cloud backup restore window.

  1. Click Databases in the top-left corner of Atlas.

  2. From the Database Deployments view, click the cluster name.

  3. Click the Backup tab.

  4. Click Backup Policy.

  5. In the Point in Time Restore Policy section, specify a Restore Window.

3

### Recover a point in time with continuous cloud backup.

  1. Click Databases in the top-left corner of Atlas.

  2. From the Database Deployments view, click on the cluster name.

  3. Click the Backup tab.

  4. Click the Point in Time Restore button on the far right side of the screen.

  5. Select either the Date & Time or Oplog Timestamp tab.

  6. Enter the desired point in time to restore from.

  7. Click the Next: Select Cluster button.

  8. Choose a project and cluster to restore to from the dropdown menus.

  9. Click the Restore button.

← Build a Resilient Application with MongoDB AtlasBuild a Multi-Tenant
Architecture →

