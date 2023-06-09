Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups snapshots delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified backup snapshot.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas backups snapshots delete <snapshotId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
snapshotId

|

string

|

true

|

Unique identifier of the snapshot you want to delete.  
  
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
  
\--force

|

|

false

|

Flag that indicates whether to skip the confirmation prompt before proceeding
with the requested action.  
  
-h, --help

|

|

false

|

help for delete  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
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

    
    
    Snapshot '<Name>' deleted  
      
  
## Examples

    
    
    # Remove the backup snapshot with the ID 5f4007f327a3bd7b6f4103c5 for the cluster named myDemo:  
      
    atlas backups snapshots delete 5f4007f327a3bd7b6f4103c5 --clusterName myDemo  
  
What is MongoDB Atlas? →

