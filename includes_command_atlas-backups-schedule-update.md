Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups schedule update

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Modify the backup schedule for the specified cluster for your project.

The backup schedule defines when MongoDB takes scheduled snapshots and how
long it stores those snapshots.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas backups schedule update [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--autoExport

|

|

false

|

Flag that enables automatic export of cloud backup snapshots to the AWS
bucket.  
  
\--clusterName

|

string

|

true

|

Name of the cluster.  
  
\--exportBucketId

|

string

|

false

|

Unique identifier that Atlas assigns to the bucket.  
  
\--exportFrequencyType

|

string

|

false

|

Frequency associated with the export policy. Value can be daily, weekly, or
monthly.  
  
-f, --file

|

string

|

false

|

Path to an optional JSON configuration file that defines backup schedule
settings.  
  
-h, --help

|

|

false

|

help for update  
  
\--noAutoExport

|

|

false

|

Flag that disables automatic export of cloud backup snapshots to the AWS
bucket.  
  
\--noUpdateSnapshots

|

|

false

|

Flag that disables applying the retention changes in the updated backup policy
to snapshots that Atlas took previously.  
  
\--noUseOrgAndGroupNamesInExportPrefix

|

|

false

|

Flag that disables usage of organization and project names instead of
organization and project UUIDs in the path for the metadata files that Atlas
uploads to your S3 bucket after it finishes exporting the snapshots.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--policy

|

stringArray

|

false

|

Array containing a document for each backup policy item in the desired updated
backup policy. You must specify it in a format: '--policy
policyID,policyItemID,frequencyType,frequencyIntervalNumber,retentionUnit,retentionValue'.  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
\--referenceHourOfDay

|

int

|

false

|

Hour of the day to schedule snapshots using a 24-hour clock. Accepted values
are between 0 and 23 inclusive.  
  
\--referenceMinuteOfHour

|

int

|

false

|

Minute of the hour to schedule snapshots. Accepted values are between 0 and 59
inclusive.  
  
\--restoreWindowDays

|

int

|

false

|

Number of days back in time you can restore to with Continuous Cloud Backup
accuracy. Must be a positive, non-zero integer. Applies to continuous cloud
backups only.  
  
\--updateSnapshots

|

|

false

|

Flag that enables applying the retention changes in the updated backup policy
to snapshots that Atlas took previously.  
  
\--useOrgAndGroupNamesInExportPrefix

|

|

false

|

Flag that enables usage of organization and project names instead of
organization and project UUIDs in the path for the metadata files that Atlas
uploads to your S3 bucket after it finishes exporting the snapshots.  
  
## Inherited Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
-P, --profile

|

string

|

false

|

Human-readable label that identifies the profile to use from your
configuration file. To learn about profiles for the Atlas CLI, see
https://dochub.mongodb.org/core/atlas-cli-save-connection-settings. To learn
about profiles for MongoCLI, see https://dochub.mongodb.org/core/atlas-cli-
configuration-file.  
  
## Output

If the command succeeds, the CLI returns output similar to the following
sample. Values in brackets represent your values.

    
    
    Snapshot backup policy for cluster '<ClusterName>' updated.  
      
  
## Examples

    
    
    # Update a snapshot backup policy for a cluster named Cluster0 to back up snapshots every 6 hours and, retain for 7 days, and update retention of previously-taken snapshots:  
      
    atlas backup schedule update --clusterName Cluster0 --updateSnapshots --policy 62da8faac84a2721e448d767,62da8faac84a2721e448d768,hourly,6,days,7  
      
    
    # Update a snapshot backup policy for a cluster named Cluster0 to export snapshots monthly to an S3 bucket:  
      
    atlas backup schedule update --clusterName Cluster0 --exportBucketId 62c569f85b7a381c093cc539 --exportFrequencyType monthly  
  
What is MongoDB Atlas? →

