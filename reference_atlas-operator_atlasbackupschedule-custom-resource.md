Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `AtlasBackupSchedule` Custom Resource

Share Feedback

On this page

  * Example
  * Parameters

The `AtlasBackupSchedule` custom resource configures a backup schedule that
you can apply to your `AtlasDeployment` Custom Resource. When you create the
`AtlasBackupSchedule` custom resource, Atlas Kubernetes Operator tries to
create or update a backup schedule.

## Important

### Custom Resources Definitions Take Priority

Atlas Kubernetes Operator uses custom resource configuration files to manage
your Atlas configuration. Each custom resource definition overrides settings
specified in other ways such as in the Atlas UI. If you delete a custom
resource, Atlas Kubernetes Operator deletes the object from Atlas unless you
use annotations to skip deletion. To learn more, see the Create and Update
Process and the Delete Process.

Atlas Kubernetes Operator does one of the following actions using the Atlas
Cloud Backup Schedule API Resource:

  * Creates a new backup schedule.

  * Updates an existing backup schedule.

If you remove the `AtlasBackupSchedule` resource from your Kubernetes cluster,
Atlas stops creating backups for your cluster.

## Note

You must do all of the following to back up a cluster:

  1. Create a backup policy

  2. Create a backup schedule and set the `spec.policy.name` field to the name of the configured backup policy.

  3. Set the `spec.backupRef.name` field in the `AtlasDeployment` Custom Resource to the name of the configured backup schedule.

To learn more, see Back Up Your Atlas Cluster.

You can specify one backup schedule per cluster, but you can use the same
backup schedule for multiple clusters.

## Example

The following example shows an `AtlasBackupSchedule` custom resource
configured to take snapshots at 10:10 UTC and restore up to two days:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasBackupSchedule  
    metadata:  
      name: atlas-default-backupschedule  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      autoExportExabled: true  
      referenceHourOfDay: 10  
      referenceMinuteOfHour: 10  
      restoreWindowDays: 2  
      policy:  
        name: atlas-default-backuppolicy  
        namespace: mongodb-atlas-system  
  
## Parameters

This section describes some of the key `AtlasBackupSchedule` custom resource
parameters available. For a full list of parameters available, see the Atlas
Modify Cloud Backup Backup Policy API. Refer to these descriptions, the
available examples, and the API documentation to customize your
specifications.

`spec.autoExportEnabled`

    

 _Type_ : boolean

 _Optional_

Flag that specifies whether Atlas automatically exports cloud backup snapshots
to your AWS backup. Specify `true` to enable automatic export of cloud backup
snapshots to the AWS bucket. Specify `false` to disable automatic export.

`spec.export`

    

 _Type_ : object

 _Optional_

Policy for automatically exporting cloud backup snapshots.

`spec.export.exportBucketId`

    

 _Type_ : string

 _Optional_

Unique 24-hexadecimal character string that identifies the AWS bucket.

`spec.export.frequencyType`

    

 _Type_ : string

 _Optional_

Human-readable label that indicates the rate at which the export policy item
occurs.

`spec.referenceHourOfDay`

    

 _Type_ : number

 _Optional_

Number that indicates the UTC hour of day between `0` and `23`, inclusive,
representing the hour of the day that Atlas takes snapshots for backup policy
items.

`spec.referenceMinuteOfHour`

    

 _Type_ : number

 _Optional_

Number that indicates the minutes after `spec.referenceHourOfDay` that Atlas
takes snapshots for backup policy items. Value must be between `0` `59`
inclusive.

`spec.restoreWindowDays`

    

 _Type_ : number

 _Optional_

Number that indicates the days back in time that you can restore to with
continuous cloud backup accuracy. Value must be a positive, non-zero integer.

This setting applies to continuous cloud backups only.

`spec.policy`

    

 _Type_ : array

 _Required_

List that contains the details for the backup policy to apply.

`spec.policy.name`

    

 _Type_ : string

 _Required_

`metadata.name` value within thhe `AtlasBackupPolicy` Custom Resource for the
backup policy that you want to apply. You can specify only one backup policy
per backup schedule. You can't use the same backup policy in multiple backup
schedules.

`spec.policy.namespace`

    

 _Type_ : string

 _Required_

String that indicates the namespace that contains the `AtlasBackupPolicy`
Custom Resource for the backup policy that you want to apply.

← `AtlasBackupPolicy` Custom Resource`AtlasTeam` Custom Resource →

