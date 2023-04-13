Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Resolve Alerts

Share Feedback

On this page

  * View Alerts
  * Acknowledge Alerts
  * Unacknowledge Alerts
  * Increase Cluster Capacity
  * View All Activity
  * Retrieve the Activity Feed
  * Resolutions for Specific Alerts

Atlas issues alerts for the database and server conditions configured in your
alert settings. When a condition triggers an alert, Atlas displays a warning
symbol on the cluster and sends alert notifications. Your alert settings
determine the notification methods. Atlas continues sending notifications at
regular intervals until the condition resolves or you delete or disable the
alert. You should fix the immediate problem, implement a long-term solution,
and view metrics to monitor your progress.

## Note

If you integrate with VictorOps, OpsGenie, or DataDog, you can recieve
informational alerts from these third-party monitoring services in Atlas.
However, you must resolve these alerts within each external service.

Organization Alerts

Project Alerts

## View Alerts

Organization Alerts

Project Alerts

You can view all alerts, alert settings, and deleted alerts on the
Organization Alerts page. To learn more, see Alerts Workflow.

To view all open alerts:

1

### Navigate to the Alerts page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Alerts in the sidebar.

2

### If it is not already displayed, click the All Alerts tab.

## Acknowledge Alerts

Organization Alerts

Project Alerts

To acknowledge alerts:

1

### Navigate to the Alerts page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Alerts in the sidebar.

2

### Select the alert you want to acknowledge, then click Mark Acknowledge.

## Important

If an alert uses PagerDuty for alert notifications, you can acknowledge the
alert only on your PagerDuty dashboard.

When you acknowledge an alert, Atlas sends no further notifications until
either the acknowledgement period ends, you resolve the alert condition, or
you unacknowledge the alert. If an alert condition ends during an
acknowledgment period, Atlas sends a notification.

## Unacknowledge Alerts

You can unacknowledge an alert that you previously acknowledged. After you
unacknowledge an active alert, Atlas resumes sending notifications at regular
intervals until the condition resolves or you delete, disable, or re-
acknowledge the alert.

Organization Alerts

Project Alerts

To unacknowledge alerts:

1

### Navigate to the Alerts page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Alerts in the sidebar.

2

### Select the alert you want to acknowledge, then click Unacknowledge on the
right side of the alert.

## Important

If an alert uses PagerDuty for alert notifications, you can acknowledge the
alert only on your PagerDuty dashboard.

## Increase Cluster Capacity

To resolve an alert by increasing your cluster's capacity, see Modify a
Cluster.

## View All Activity

To view and filter the activity feed for an organization or project, see View
the Activity Feed.

## Retrieve the Activity Feed

Organization Alerts

Project Alerts

You can retrieve events for an organization using the get all API resource.

## Resolutions for Specific Alerts

The following sections describe Atlas alert conditions and suggest steps for
resolving them.

Alert Type

|

Description  
  
|  
  
Atlas Search Alerts

|

Amount of CPU and memory used by Atlas Search processes reach a specified
threshold.  
  
Connection Alerts

|

Number of connections to a MongoDB process exceeds the allowable maximum.  
  
Disk Utilization % Alerts

|

Percentage of disk IOPS utilized reaches a specified threshold.  
  
Disk Space % Used Alerts

|

Percentage of used disk space on a partition reaches a specified threshold.  
  
Query Targeting Alerts

|

Indicates inefficient queries.

## Note

The changestream cursors that the Atlas Search process (`mongot`) uses for
replication can contribute to the query targeting ratio and trigger query
targeting alerts if the ratio is high.  
  
Replica Set Has No Primary

|

No primary is detected in replica set.  
  
Replication Oplog Alerts

|

Amount of oplog data generated on a primary cluster member is larger than the
cluster's configured oplog size.  
  
System CPU Usage Alerts

|

CPU usage of the MongoDB process reaches a specified threshold.  
  
← Configure Alert SettingsFix Atlas Search Issues →

