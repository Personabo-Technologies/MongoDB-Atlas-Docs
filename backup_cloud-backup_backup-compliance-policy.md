Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure a Backup Compliance Policy

Share Feedback

On this page

  * Prohibited Actions
  * Considerations
  * Prerequisites
  * Procedure
  * View Projects that have a Backup Compliance Policy Enabled

If you have strict data protection requirements, you can enable a Backup
Compliance Policy to protect your backup data.

## Important

### You Can't Disable a Backup Compliance Policy

After you enable a Backup Compliance Policy, you can't disable it without
MongoDB support. To disable a Backup Compliance Policy, the security or legal
representative specified for the Backup Compliance Policy must request support
and complete an extensive verification process. Before you enable a Backup
Compliance Policy, carefully review the prohibited actions and considerations.
You can re-enable a Backup Compliance Policy at any time.

## Prohibited Actions

If you enable a Backup Compliance Policy, no user, regardless of role, can do
the following actions:

  * Disable the Backup Compliance Policy without MongoDB support. To disable a Backup Compliance Policy, the security or legal representative specified for the Backup Compliance Policy must request support and complete an extensive verification process.

  * Modify the backup policy for an individual cluster below the minimum requirements set in the Backup Compliance Policy.

  * Delete a backup snapshot.

  * Decrease the retention time for a snapshot after it's taken.

  * Disable Cloud Backup.

  * Disable Continuous Cloud Backup if the Backup Compliance Policy has the Require Point in Time Restore to all clusters option set to On without MongoDB Support. To disable Continuous Cloud Backup, the security or legal representative specified for the Backup Compliance Policy must request support and complete an extensive verification process.

  * Reduce the Continuous Cloud Backup Restore Window without MongoDB Support. To reduce the Continuous Cloud Backup Restore Window, the security or legal representative specified for the Backup Compliance Policy must request support and complete an extensive verification process.

  * Delete policy items specified in the Backup Compliance Policy without MongoDB Support. To delete policy items specified in the Backup Compliance Policy, the security or legal representative specified for the Backup Compliance Policy must request support and complete an extensive verification process.

  * Delete the project if any snapshots exist. If you can't remove all projects, you can't delete the organization.

## Considerations

After you enable a Backup Compliance Policy, the following behaviors apply:

  * A Backup Compliance Policy limits your ability to reduce backup storage costs. You can't adjust the retention or delete a backup to reduce the backup storage costs. To learn more, see Manage Billing.

  * All new and existing clusters have Cloud Backup automatically enabled and use the project-level Backup Compliance Policy. Atlas augments any preexisting cluster-level backup policies to meet the minimum requirements of the Backup Compliance Policy. All new clusters use the Backup Compliance Policy unless the mininum requirements of the cluster-level backup policy expand beyond the mininum requirements of the Backup Compliance Policy.

  * You can modify the cluster-level backup policies at any time. If you reduce the frequency of a cluster-level backup policy, the change applies only to future backups. Any existing oplog remains for the original window. The minimum requirements of the Backup Compliance Policy apply.

  * If the Backup Compliance Policy has the Keep all snapshots when removing additional snapshot regions option set to On and you enable, modify, or delete multi-region snapshots, any snapshots already taken remain.

  * When you resume a cluster, Atlas automatically enables Cloud Backup. If the Backup Compliance Policy has the Require Point in Time Restore to all clusters option set to On, Atlas automatically enables Continuous Cloud Backup and adjusts the restore window according to the Backup Compliance Policy. Atlas automatically modifies the backup to meet the minimum requirements of the Backup Compliance Policy.

  * If you terminate a cluster, Atlas maintains all existing snapshots after the termination according to your backup policy. Atlas retains the oplog for restoring a point in time with continuous cloud backup in a static state until Atlas can no longer use them for continuous cloud backup.

  * Whenever a user enables, modifies, or disables a Backup Compliance Policy, Atlas reflects the event in the Project Activity Feed.

## Prerequisites

  * You must have the `Project Owner` role for the project or the `Organization Owner` role for its parent organization.

  * Only MongoDB Support can do the following actions:

    * Disable the Backup Compliance Policy.

    * Disable Continuous Cloud Backup if the Backup Compliance Policy has the Require Point in Time Restore to all clusters option set to On.

    * Reduce the Continuous Cloud Backup Restore Window.

    * Delete policy items specified in the Backup Compliance Policy.

  * Only the specified security or legal representative can request support.

  * You can apply a Backup Compliance Policy to `M10+` dedicated clusters only.

## Note

You can't convert a dedicated cluster to a `M0` free clusters, an `M2` or `M5`
shared cluster, or a serverless instance.

## Procedure

1

### Enable the Backup Compliance Policy.

## Important

### You Can't Disable a Backup Compliance Policy

After you enable a Backup Compliance Policy, you can't disable it without
MongoDB support. To disable a Backup Compliance Policy, the security or legal
representative specified for the Backup Compliance Policy must request support
and complete an extensive verification process. Before you enable a Backup
Compliance Policy, carefully review the prohibited actions and considerations.
You can re-enable a Backup Compliance Policy at any time.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Next to the Projects menu, expand the Options menu, then click Project Settings.

  4. Toggle Data Protection Policy to On.

The Edit Data Protection Policy dialog opens.

## Note

This Backup Compliance Policy applies as the minimum backup policy to all
clusters in the project. The Backup Compliance Policy protects all existing
snapshots. The Backup Compliance Policy prevents any user, regardless of role,
from modifying or deleting existing snapshots prior to their expiration.
Changes made to this Backup Compliance Policy apply only to future snapshots.
If you enable a Backup Compliance Policy, the Backup Compliance Policy limits
your ability to reduce backup storage costs. You can't adjust the retention or
delete a backup to reduce the backup storage costs.

2

Each row in the Backup Policy Frequency and Retention table represents a
backup policy item.

## Important

After you save the Backup Compliance Policy, you can't delete policy items
specified in the Backup Compliance Policy without MongoDB Support. To delete
policy items specified in the Backup Compliance Policy, the security or legal
representative specified for the Backup Compliance Policy must request support
and complete an extensive verification process. Ensure that you have the
correct policy items before you save the Backup Compliance Policy.

  1. Do one of the following steps:

    * Select the frequency unit from Frequency Unit for a policy item.

    * Click Add Frequency Unit to add a new policy item to your backup policy.

  2. Select the frequency for the frequency unit from the Every column.

  3. Specify the retention time for the policy item in the Retention Time column and the units for the retention time in the column to the right.

3

### (Optional) Configure the restore window.

  1. Toggle Require Point in Time Restore to all clusters to On.

  2. Specify a Restore Window.

## Important

You can't configure a restore window that is longer than the Hourly Snapshot
Retention Time. After you save this Backup Compliance Policy, you can't change
this setting without MongoDB support. To change this setting, the security or
legal representative specified for the Backup Compliance Policy must request
support and complete an extensive verification process.

4

### (Optional) Require Encryption at Rest using Customer Key Management for
all clusters

Toggle Require Encryption at Rest using Customer Key Management for all
clusters to On.

## Note

To enable this option, you must Enable Encryption at Rest for all current
clusters. You can't enable this option on paused clusters that don't have
Encryption at Rest enabled.

5

### (Optional) Keep all snapshots when removing additional snapshot regions.

You can prevent cluster users from deleting backups copied to other regions
even if you change the Copy to other regions option to Off. To learn more, see
Configure Atlas to Automatically Copy Snapshots to Other Regions.

  * Toggle Keep all snapshots when removing additional snapshot regions to On.

6

### Confirm and save the Backup Compliance Policy.

  1. Click Next.

## Important

### You Can't Disable a Backup Compliance Policy

After you enable a Backup Compliance Policy, you can't disable it without
MongoDB support. To disable a Backup Compliance Policy, the security or legal
representative specified for the Backup Compliance Policy must request support
and complete an extensive verification process. Before you enable a Backup
Compliance Policy, carefully review the prohibited actions and considerations.
You can re-enable a Backup Compliance Policy at any time.

  2. Specify the Email address of a security or legal representative.

  3. If you are _sure_ that you want to save the Backup Compliance Policy, specify the project name to continue.

  4. Click the checkbox to confirm that you understand that when you enable a Backup Compliance Policy, no user, regardless of role, can modify or delete backup snapshots. If you enable a Backup Compliance Policy, the Backup Compliance Policy limits your ability to reduce backup storage costs and you can _not_ adjust the retention or delete a backup to reduce backup storage costs. Only MongoDB Support can disable a Backup Compliance Policy. Only the specified security or legal representative can request support to disable a Backup Compliance Policy.

  5. Click Confirm and Save.

## View Projects that have a Backup Compliance Policy Enabled

A Backup Compliance Policy icon appears next to each project name that has a
Backup Compliance Policy enabled.

1

### View all of your projects.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. Click the Leaf icon in the upper left corner of the page. You can also expand the Projects menu in the navigation bar, then click View All Projects.

← Backup Scheduling, Retention, and On-Demand SnapshotsStorage Engine and
Cloud Backup Encryption →

