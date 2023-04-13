Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas security ldap delete

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the current LDAP configuration captured in the userToDNMapping document
from your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas security ldap delete [options]  
      
  
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

    
    
    LDAP configuration userToDNMapping deleted from project'<Name>'  
      
  
## Examples

    
    
    # Remove the current LDAP configuration in the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas security ldap delete --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

