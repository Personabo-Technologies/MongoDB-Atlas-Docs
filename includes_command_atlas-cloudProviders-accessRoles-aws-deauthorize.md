Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas cloudProviders accessRoles aws deauthorize

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options

Deauthorize an AWS IAM role.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas cloudProviders accessRoles aws deauthorize <roleId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
roleId

|

string

|

true

|

Unique ID of the role to authorize.  
  
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

help for deauthorize  
  
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
  
What is MongoDB Atlas? →

