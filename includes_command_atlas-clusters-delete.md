Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified cluster from your project.

The command prompts you to confirm the operation when you run the command
without the --force option.

Deleting a cluster also deletes any backup snapshots for that cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas clusters delete <clusterName> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
clusterName

|

string

|

true

|

Name of the cluster to delete.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
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

    
    
    Cluster '<Name>' deleted  
      
  
## Examples

    
    
    # Remove a cluster named myCluster after prompting for a confirmation:  
      
    atlas clusters delete myCluster  
      
    
    # Remove a cluster named myCluster without requiring confirmation:  
      
    atlas clusters delete myCluster --force  
  
What is MongoDB Atlas? →

