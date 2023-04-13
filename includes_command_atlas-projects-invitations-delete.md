Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects invitations delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified pending invitation to your project.

To use this command, you must authenticate with a user account or an API key
that has the Project User Admin role.

## Syntax

    
    
    atlas projects invitations delete <invitationId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
invitationId

|

string

|

true

|

Unique 24-digit string that identifies the invitation.  
  
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

    
    
    Invitation '<Name>' deleted  
      
  
## Examples

    
    
    # Remove the pending invitation with the ID 5dd56c847a3e5a1f363d424d from the project with the ID 5f71e5255afec75a3d0f96dc:  
      
    atlas projects invitations delete 5dd56c847a3e5a1f363d424d --projectId 5f71e5255afec75a3d0f96dc  
  
What is MongoDB Atlas? →

