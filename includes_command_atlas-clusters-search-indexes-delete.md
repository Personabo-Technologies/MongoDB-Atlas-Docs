Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters search indexes delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Delete the specified search index from the specified cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Data Access Admin role.

## Syntax

    
    
    atlas clusters search indexes delete <indexId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
indexId

|

string

|

true

|

ID of the index.  
  
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

    
    
    Index '<Name>' deleted  
      
  
## Examples

    
    
    # Delete the search index with the ID 5f2099cd683fc55fbb30bef6 for the cluster named myCluster without requiring confirmation:  
      
    atlas clusters search indexes delete 5f2099cd683fc55fbb30bef6 --clusterName myCluster --force  
  
What is MongoDB Atlas? →

