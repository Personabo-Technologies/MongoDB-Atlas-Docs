Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas projects delete <ID> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
ID

|

string

|

true

|

Unique 24-digit string that identifies the project.  
  
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

    
    
    Project '<Name>' deleted  
      
  
## Examples

    
    
    # Remove the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas projects delete 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

