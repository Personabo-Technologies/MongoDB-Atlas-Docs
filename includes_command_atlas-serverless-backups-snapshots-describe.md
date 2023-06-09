Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas serverless backups snapshots describe

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return the details for the specified snapshot for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas serverless backups snapshots describe [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--clusterName

|

string

|

true

|

Name of the cluster.  
  
-h, --help

|

|

false

|

help for describe  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
\--snapshotId

|

string

|

true

|

Unique identifier of the snapshot to restore. You must specify a snapshotId
for automated restores.  
  
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
  
## Examples

    
    
    # Return the details for the backup snapshot with the ID 5f4007f327a3bd7b6f4103c5 for the instance named myDemo:  
      
    atlas serverless backups snapshots describe --snapshotId 5f4007f327a3bd7b6f4103c5 --clusterName myDemo  
  
What is MongoDB Atlas? →

