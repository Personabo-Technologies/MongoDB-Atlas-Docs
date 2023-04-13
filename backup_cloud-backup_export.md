Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Export Cloud Backup Snapshot

Share Feedback

On this page

  * How Atlas Exports Snapshots
  * Exported Data Format
  * Limitations
  * Prerequisites
  * Export Management

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

Atlas lets you export your Cloud Backup snapshots to an AWS S3 bucket.

## How Atlas Exports Snapshots

You can manually export individual snapshots or set up an export policy for
automatic export of your snapshots. For automatic exports, you must specify a
frequency in your export policy:

  * Daily

  * Weekly

  * Monthly

Atlas automatically exports any backup snapshot with the frequency type that
matches the export frequency. The exported result is a full backup of that
snapshot.

## Example

Consider the following:

  * A backup policy that sets a weekly and monthly snapshot schedule

  * An export policy that sets a monthly export frequency

Suppose, at the end of the month, the weekly and monthly snapshots happen on
the same day. There would be `4` snapshots of which `3` would be weekly
snapshots and the fourth snapshot, although treated as a weekly snapshot by
Atlas, would also be the monthly snapshot because it happened on the same day.
Atlas will export the monthly snapshot only because the export frequency
matches the snapshot frequency for that snapshot. To export the weekly
snapshots as well, update the export policy to export weekly snapshots also.
If the export frequency is set to weekly, Atlas would export all `4`
snapshots.

Atlas exports snapshots for collections one at a time. As the export
progresses, you may see partial results in your S3 bucket. Atlas queues any
new job if Atlas is currently exporting 5 or more replica sets. For sharded
clusters, Atlas always exports the snapshots of all the shards simultaneously,
regardless of the number of shards.

Atlas charges `$.125` per GB of data exported to the AWS S3 bucket, in
addition to the data transfer cost incurred from AWS itself. Atlas compresses
the data before exporting. To estimate the amount of data being exported, add
up the dataSize of each database in your cluster. This total should correspond
to the uncompressed size of your export, which would be the maximum cost
incurred from Atlas for the data export operation.

### Files Atlas Uploads

Atlas uploads an empty file to `/exported_snapshots/.permissioncheck` when
you:

  * Add a new AWS S3 export bucket

  * Start an export

After Atlas finishes exporting, Atlas uploads a metadata file named
`.complete` and a metadata file named `metadata.json` for each collection.

.complete File

metadata.json File

Atlas uploads the metadata file named `.complete` in the following path on
your S3 bucket:

    
    
    /exported_snapshots/<orgUUID>/<projectUUID>/<clusterName>/<initiationDateOfSnapshot>/<timestamp>/  
      
  
## Note

By default, Atlas uses organization and project UUIDs in the path for the
metadata files. To use organization and project names instead of UUIDs, set
the `useOrgAndGroupNamesInExportPrefix` flag to `true` via the API. Atlas
replaces any spaces with underscores (`_`) and removes any characters that
might require special handling and characters to avoid from the organization
and project names in the path.

The `.complete` metadata file is in JSON format and contains the following
fields:

Field

|

Description  
  
|  
  
`orgId`

|

Unique 24-hexadecimal digit string that identifies the Atlas organization.  
  
`orgName`

|

Name of the Atlas organization.  
  
`groupId`

|

Unique 24-hexadecimal digit string that identifies the project in the Atlas
organization.  
  
`groupName`

|

Name of the Atlas project.  
  
`clusterUniqueId`

|

Unique 24-hexadecimal digit string that identifies the Atlas cluster.  
  
`clusterName`

|

Name of the Atlas project.  
  
`snapshotInitiationDate`

|

Date when snapshot was taken.  
  
`totalFiles`

|

Total number of files uploaded to the S3 bucket.  
  
`labels`

|

Labels of the cluster whose snapshot was exported.  
  
`customData`

|

Custom data, if any, that you specified when creating the export job.  
  
## Example

    
    
    {  
      
      "orgId": "60512d6f65e4047fe0842095",  
      "orgName": "org1",  
      "groupId": "60512dac65e4047fe084220f",  
      "groupName": "group1",  
      "clusterUniqueId": "60512dac65e4047fe0842212",  
      "clusterName": "cluster0",  
      "snapshotInitiationDate": "2020-04-03T05:50:29.321Z"  
      "totalFiles": 23,  
      "labels": [  
        {  
          "key": "key1",  
          "value": "xyz"  
        },  
        {  
          "key": "key2",  
          "value": "xyzuio"  
        }  
      ],  
      "customData": [  
        {  
          "key": "key1",  
          "value": "xyz"  
        },  
        {  
          "key": "key2",  
          "value": "xyzuio"  
        }  
      ]  
    }  
  
If an export job fails:

  * Atlas doesn't automatically try to export again.

  * Atlas doesn't remove any partial data in your S3 bucket.

## Exported Data Format

Atlas uploads the contents of your database to S3 in `.json.gz` format with
documents in extended JSON format within. The path to the files on S3 is:

    
    
    /exported_snapshots/<orgName>/<projectName>/<clusterName>/<initiationDateOfSnapshot>/<timestamp>/<dbName>/<collectionName>/<shardName>.<increment>.json.gz  
      
  
Where:

|  
  
|  
  
`<orgName>`

|

Name of your Atlas organization.  
  
`<projectName>`

|

Name of your Atlas project.  
  
`<clusterName>`

|

Name of your Atlas cluster.  
  
`<initiationDateOfSnapshot>`

|

Date when snapshot was taken.  
  
`<timestamp>`

|

Timestamp when the export job was created.  
  
`<dbName>`

|

Name of the database in the Atlas cluster.  
  
`<collectionName>`

|

Name of the Atlas collection.  
  
`<shardName>`

|

Name of the replica set.  
  
`<increment>`

|

Count that is incremented as chunks are uploaded. Starts at `0`.  
  
## Limitations

The following limitations apply:

  * You can only export to AWS S3 buckets.

  * You can only export snapshots for currently supported versions of MongoDB, but you can always download saved snapshots, regardless of the version.

  * You can't export fallback snapshots.

  * You can have only one active export per snapshot.

## Important

When you export snapshots from a sharded cluster to S3 buckets, the export
from each shard might have a different timestamp. This can result in duplicate
or inconsistent data across the shards.

## Prerequisites

To export your Cloud Backup snapshots to an AWS S3 bucket, you will need the
following:

  1. `M10` or higher Atlas cluster with Cloud Backup enabled.

  2. AWS IAM role with `STS:AssumeRole` that grants Atlas access to your AWS resources. To learn more about configuring AWS access for Atlas, see Set Up Unified AWS Access.

  3. AWS IAM role policy that grants Atlas write access or the `S3:PutObject` and `S3:GetBucketLocation` permissions to your AWS resources. To learn more about configuring write access to AWS resources, see Set Up Unified AWS Access.

## Example

    
        {  
      
      "Version": "2012-10-17",  
      "Statement": [  
        {  
          "Effect": "Allow",  
          "Action": "s3:GetBucketLocation",  
          "Resource": "arn:aws:s3:::bucket-name"  
        },  
        {  
          "Effect": "Allow",  
          "Action": "s3:PutObject",  
          "Resource": "arn:aws:s3:::bucket-name/*"  
        }  
      ]  
    }  
  

## Export Management

Atlas CLI

Atlas Administration API

### Manage Export Jobs

You can manage export jobs using the Atlas CLI by creating or viewing export
jobs.

#### Create an Export Job

To export one backup snapshot for an M10 or higher Atlas cluster to an
existing AWS S3 bucket using the Atlas CLI, run the following command:

    
    
    atlas backups exports jobs create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas backups exports jobs create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

#### View Export Jobs

To list the cloud backup restore jobs for the project you specify using the
Atlas CLI, run the following command:

    
    
    atlas backups exports jobs list <clusterName> [options]  
      
  
To return the details for the cloud backup restore job you specify using the
Atlas CLI, run the following command:

    
    
    atlas backups exports jobs describe [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas backups exports jobs list and atlas
backups exports jobs describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Manage Export Buckets

You can manage export buckets using the Atlas CLI by creating, viewing, or
deleting export buckets.

#### Create an Export Bucket

To create an export destination for Atlas backups using an existing AWS S3
bucket using the Atlas CLI, run the following command:

    
    
    atlas backups exports buckets create <bucketName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas backups exports buckets create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

#### View Export Buckets

To list the cloud backup restore buckets for the project you specify using the
Atlas CLI, run the following command:

    
    
    atlas backups exports buckets list [options]  
      
  
To return the details for the cloud backup restore bucket you specify using
the Atlas CLI, run the following command:

    
    
    atlas backups exports buckets describe [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas backups exports buckets list and atlas
backups exports buckets describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

#### Delete an Export Bucket

To delete an export destination for Atlas backups using the Atlas CLI, run the
following command:

    
    
    atlas backups exports buckets delete [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas backups exports buckets delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Storage Engine and Cloud Backup EncryptionRestore Your Database Deployment →

