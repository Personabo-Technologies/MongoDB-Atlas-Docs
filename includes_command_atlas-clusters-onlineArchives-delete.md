Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters onlineArchives delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified online archive from your cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Data Access Admin role.

## Syntax

    
    
    atlas clusters onlineArchives delete <archiveId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
archiveId

|

string

|

true

|

Unique identifier of the online archive to delete.  
  
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

    
    
    Archive '<Name>' deleted  
      
  
## Examples

    
    
    # Remove an online archive with the ID 5f189832e26ec075e10c32d3 for the cluster named myCluster:  
      
    atlas clusters onlineArchives delete 5f189832e26ec075e10c32d3 --clusterName myCluster  
  
What is MongoDB Atlas? →

