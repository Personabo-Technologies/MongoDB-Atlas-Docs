Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Serverless Instance Backup

Share Feedback

On this page

  * Go to the serverless instance settings.
  * Modify the Backup settings.
  * Save your changes.

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
  
To modify the backup option for your serverless instance:

1

## Go to the serverless instance settings.

For the serverless instance to modify, click the ellipses ... icon and select
Edit Configuration.

2

## Modify the Backup settings.

Select Serverless Continuous Backup or Basic Backup.

## Note

If you change from Serverless Continuous Backup to Basic Backup, a dialog
appears to confirm that you want to disable Serverless Continuous Backup.
Click Disable.

3

## Save your changes.

  1. Click Review Changes.

  2. Click Apply Changes.

← Manage Serverless InstancesTerminate a Serverless Instance →

