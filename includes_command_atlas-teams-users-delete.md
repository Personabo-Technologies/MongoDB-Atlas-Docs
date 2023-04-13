Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas teams users delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified user from a team for your organization.

To use this command, you must authenticate with a user account or an API key
that has the Organization User Admin role.

## Syntax

    
    
    atlas teams users delete <userId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
userId

|

string

|

true

|

Unique 24-digit string that identifies the user.  
  
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
  
\--orgId

|

string

|

false

|

Organization ID to use. Overrides the settings in the configuration file or
environment variable.  
  
\--teamId

|

string

|

true

|

Unique 24-digit string that identifies the team.  
  
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

    
    
    User '<Name>' deleted from the team  
      
  
## Examples

    
    
    # Remove the user with the ID 5dd58c647a3e5a6c5bce46c7 from the team with the ID 5f6a5c6c713184005d72fe6e for the organization with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas teams users delete 5dd58c647a3e5a6c5bce46c7 --teamId 5f6a5c6c713184005d72fe6e --orgId 5e1234c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

