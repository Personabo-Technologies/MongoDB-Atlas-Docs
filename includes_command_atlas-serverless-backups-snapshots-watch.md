Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas serverless backups snapshots watch

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Watch the specified snapshot in your project until it reaches a completed or
failed status.

This command checks the snapshot's status periodically until it reaches a
completed or failed status. Command finishes once one of the expected statuses
are reached. If you run the command in the terminal, it blocks the terminal
session until the resource status completes or fails. You can interrupt the
command's polling at any time with CTRL-C. To use this command, you must
authenticate with a user account or an API key that has the Project Read Only
role.

## Syntax

    
    
    atlas serverless backups snapshots watch [options]  
      
  
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

help for watch  
  
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

    
    
    # Watch the backup snapshot with the ID 5f4007f327a3bd7b6f4103c5 in the cluster named myDemo until it becomes available:  
      
    atlas backups snapshots watch 5f4007f327a3bd7b6f4103c5 --clusterName myDemo  
  
What is MongoDB Atlas? →

