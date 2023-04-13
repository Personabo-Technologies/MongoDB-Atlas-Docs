Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `AtlasBackupPolicy` Custom Resource

Share Feedback

On this page

  * Example
  * Parameters

The `AtlasBackupPolicy` custom resource configures a backup policy that
applies to the `AtlasBackupSchedule` Custom Resource that you can apply to
your `AtlasDeployment` Custom Resource. When you create the
`AtlasBackupPolicy` custom resource, Atlas Kubernetes Operator tries to create
or update a backup policy.

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

  * Creates a new backup policy.

  * Updates an existing backup policy.

If you remove the `AtlasBackupPolicy` resource from your Kubernetes cluster,
Atlas stops creating backups for your cluster.

## Note

You must do all of the following tasks to back up a cluster:

  1. Create a backup policy.

  2. Create a backup schedule and set the `spec.policy.name` field to the name of the configured backup policy.

  3. Set the `spec.backupRef.name` field in the `AtlasDeployment` Custom Resource to the name of the configured backup schedule.

To learn more, see Back Up Your Atlas Cluster.

## Example

The following example shows an `AtlasBackupPolicy` custom resource that is
configured to take snapshots weekly and retain snapshots for seven days:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasBackupPolicy  
    metadata:  
      name: "atlas-default-backuppolicy"  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      items:  
        frequencyType: "weekly"  
        frequencyInterval: 1  
        retentionUnit: "days"  
        retentionValue: 7  
  
## Parameters

This section describes some of the key `AtlasBackupPolicy` custom resource
parameters available. For a full list of parameters available, see the Atlas
Modify Cloud Backup Backup Policy API. Refer to these descriptions, the
available examples, and the API documentation to customize your
specifications.

`spec.items`

    

 _Type_ : array

 _Conditional_

List that contains the policy item parameters from the API. For a full list of
parameters available, see the Atlas Modify Cloud Backup Backup Policy API.

`spec.items.frequencyInterval`

    

 _Type_ : number

 _Required_

Number that indicates the desired frequency of the new backup policy item
specified by `spec.items.frequencyType`. A value of `1` specifies the first
instance of the corresponding `spec.items.frequencyType`.

## Example

  * In a monthly policy item, `1` indicates that the monthly snapshot occurs on the first day of the month.

  * In a weekly policy item, `1` indicates that the weekly snapshot occurs on Monday.

This setting accepts the following frequency values:

  * Hourly: `1`, `2`, `4`, `6`, `8`, and `12`.

  * Daily: `1`.

  * Weekly: `1` through `7`, where `1` is Monday and `7` is Sunday.

  * Monthly: `1` through `28` and `40`, where `1` is the first day of the month and `40` is the last day of the month.

`spec.items.frequencyType`

    

 _Type_ : string

 _Required_

String that indicates the frequency associated with the backup policy item.
Accepted values are: `hourly`, `daily`, `weekly`, or `monthly`.

## Note

You can't specify multiple `hourly` and `daily` backup policy items.

`spec.items.retentionUnit`

    

 _Type_ : string

 _Required_

String that indicates the scope of the backup policy item. Together with
`spec.items.retentionValue`, these settings define the length of time to
retain snapshots. Accepted values are: `days`, `weeks`, or `months`.

`spec.items.retentionValue`

    

 _Type_ : string

 _Required_

String that indicates the value to associate with `spec.items.retentionUnit`.
Together with `spec.items.retentionUnit`, these settings define the length of
time to retain snapshots.

← `AtlasDatabaseUser` Custom Resource`AtlasBackupSchedule` Custom Resource →

