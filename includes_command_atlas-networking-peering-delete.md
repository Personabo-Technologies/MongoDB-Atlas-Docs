Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas networking peering delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified peering connection from your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas networking peering delete <peerId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
peerId

|

string

|

true

|

Unique ID of the network peering connection that you want to delete.  
  
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

    
    
    Peering connection '<Name>' deleted  
      
  
## Examples

    
    
    # Remove the network peering connection with the ID 5f60c5bd0948295c093565ba in the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas networking peering delete 5f60c5bd0948295c093565ba --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

