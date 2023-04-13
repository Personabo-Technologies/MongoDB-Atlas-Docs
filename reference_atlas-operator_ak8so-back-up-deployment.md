Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Back Up Your Atlas Cluster

Share Feedback

On this page

  * Considerations
  * Limitations
  * Prerequisites
  * Procedure
  * Create the backup policy.
  * Create the backup schedule.
  * Apply the backup schedule to the cluster.

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

## Note

### Serverless instances back up automatically

Atlas automatically enables backups for serverless instances and takes
snapshots every six hours. Any Atlas Kubernetes Operator backup custom
resources you apply to a serverless instance will not override the automatic
settings.

To learn more about backups for serverless instances, see Serverless Instance
Backups.

Atlas Kubernetes Operator supports cloud backup for your Atlas clusters. Cloud
backup uses the native snapshot capabilities of your cloud provider to support
full-copy snapshots and localized snapshot storage.

To manage cloud backup with Atlas Kubernetes Operator, you can specify and
update the following custom resources:

Custom Resource

|

Purpose  
  
|  
  
`AtlasBackupPolicy` Custom Resource

|

Defines the backup policy, including the frequency of backups and the length
of snapshot retention.  
  
`AtlasBackupSchedule` Custom Resource

|

Defines the backup schedule, including the time of day that Atlas backs up
your database deployment, the number of days back in time to which you can
restore, and the backup policy.  
  
`AtlasDeployment` Custom Resource

|

Defines the characteristics of a cluster. You must set the
`spec.backupRef.name` field to the name of the configured backup schedule to
enable cloud backup for the cluster.

Additionally, to configure continuous backup, you must set one of the
following fields to `true`:

  * `spec.deploymentSpec.pitEnabled` for standard clusters.

  * `spec.advancedDeploymentSpec.pitEnabled` for advanced clusters.

  
  
Each time you change any of the supported custom resources, Atlas Kubernetes
Operator creates or updates the corresponding Atlas configuration.

## Considerations

Review the following considerations:

  * You can specify one backup policy per backup schedule.

  * You can specify one backup schedule per cluster, but you can use the same backup schedule for multiple clusters.

  * Atlas determines the order of nodes to snapshot based on your cluster configuration. To learn more, see Cloud Backups.

## Limitations

Certain limitations apply to cloud backup. To learn more, see Back Up Your
Database Deployment.

## Prerequisites

To enable cloud backup for your Atlas Kubernetes Operator-managed cluster, you
must:

  * Have a running Kubernetes cluster with Atlas Kubernetes Operator deployed.

  * Ensure your IP address is in the organization's API access list.

## Procedure

Follow these steps to enable cloud backup for your Atlas Kubernetes Operator-
managed clusters:

1

### Create the backup policy.

To learn more about the parameters for a backup policy, see
`AtlasBackupPolicy` Custom Resource.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
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
     EOF  
  
2

### Create the backup schedule.

In the `spec.policy.name` field, specify the `metadata.name` from the
`AtlasBackupPolicy` Custom Resource to apply your backup policy.

To learn more about the other parameters for a backup schedule see
`AtlasBackupSchedule` Custom Resource.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasBackupSchedule  
    metadata:  
      name: "atlas-default-backupschedule"  
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
    EOF  
  
3

### Apply the backup schedule to the cluster.

In the `spec.backupRef.name` field of the `AtlasDeployment` Custom Resource,
specify the `metadata.name` from the `AtlasBackupSchedule` Custom Resource to
apply your backup schedule to the cluster.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasDeployment  
    metadata:  
      name: my-atlas-cluster  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      backupRef:  
        name: atlas-default-backupschedule  
        namespace: mongodb-atlas-system  
    EOF  
  
← Configure Audit LogsIntegrate with Third-Party Services →

