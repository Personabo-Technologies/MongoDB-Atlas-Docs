Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure and Resolve Alerts

Share Feedback

On this page

  * Alert Conditions
  * Configure Alerts
  * Resolve Alerts
  * Alerts Workflow

Atlas issues alerts for the database and server conditions configured in your
alert settings. When a condition triggers an alert, Atlas displays a warning
symbol on the cluster and sends alert notifications. Your alert settings
determine the notification methods. Atlas continues sending notifications at
regular intervals until the condition resolves or you delete or disable the
alert.

## Alert Conditions

When you configure alerts, you specify alert conditions and thresholds. Review
the possible alert conditions for which you can trigger alerts related to your
clusters.

## Note

`M0` free clusters and `M2/M5` shared clusters only trigger alerts related to
the metrics supported by those clusters. See Atlas M0 (Free Cluster), M2, and
M5 Limitations for complete documentation on `M0/M2/M5` alert and metric
limitations.

## Configure Alerts

To set which conditions trigger alerts and how users are notified, Configure
Alert Settings. You can configure alerts at the organization or project level.
Atlas provides default alerts at the project level. You can clone existing
alerts and configure maintenance window alerts.

## Resolve Alerts

When a condition triggers an alert, Atlas displays a warning symbol on the
cluster and sends alert notifications. Resolve these alerts and work to
prevent alert conditions from occurring in the future. To learn how to fix the
immediate problem, implement a long-term solution, and monitor your progress,
see Resolve Alerts.

## Alerts Workflow

When an alert condition is met, the following alert lifecycle begins:

1

### The alert condition is met.

  * For informational alerts like the `User joined the organization` alert, Atlas sends notifications as soon as the condition is met. These alerts don't appear in the Atlas UI. The informational alerts workflow ends here.

  * Otherwise, Atlas retrieves metrics at regular intervals based on granularity. When the retrieved metrics indicate that an alert condition is met, Atlas tracks the alert condition until it ends, or until it remains past the amount of time specified in the send if condition lasts at least field.

## Note

If the alert condition ends between sampling periods, Atlas doesn't track the
alert condition or send any notifications.

2

### The alert condition remains past the amount of time specified in the send
if condition lasts at least field.

Atlas sends notifications. The alerts appear on the All Alerts tab
(organization alerts) or the Open Alerts tab (project alerts).

3

### The alert remains active until it resolves, or you disable or delete it.

The following stages might occur:

  * You acknowledge the alert. Atlas sends no further notifications until either the acknowledgement period ends, you resolve the alert condition, or you unacknowledge the alert. If an alert condition ends during an acknowledgment period, Atlas sends a notification.

  * You unacknowledge an alert that you previously acknowledged. After you unacknowledge an active alert, Atlas resumes sending notifications at regular intervals until the condition resolves or you delete, disable, or re-acknowledge the alert.

  * You disable the alert. Atlas cancels active alerts related to the setting. A disabled alert setting remains visible but grayed-out and you can later re-enable it.

  * You enable an alert that you previously disabled.

  * You delete the alert. Atlas cancels active alerts related to the setting. A deleted alert setting does not remain visible.

  * The alert condition resolves. The alert appears on the All Alerts tab (organization alerts) or the Closed Alerts tab (project alerts).

← Use Atlas Search for Full-Text Search QueriesReview Alert Conditions →

