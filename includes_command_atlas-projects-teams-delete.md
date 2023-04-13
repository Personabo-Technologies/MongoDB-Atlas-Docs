Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects teams delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified team from your project.

After you remove a team from your project, the team still exists in the
organization in which it was created.

To use this command, you must authenticate with a user account or an API key
that has the Project User Admin role.

## Syntax

    
    
    atlas projects teams delete <teamId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
teamId

|

string

|

true

|

Unique 24-digit string that identifies the team.  
  
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

    
    
    Team '<Name>' deleted  
      
  
## Examples

    
    
    # Remove the team with the ID 5dd58c647a3e5a6c5bce46c7 from the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas projects teams delete 5dd58c647a3e5a6c5bce46c7 --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

