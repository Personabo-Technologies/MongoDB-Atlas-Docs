Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects invitations invite

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Invite the specified MongoDB user to your project.

To use this command, you must authenticate with a user account or an API key
that has the Project User Admin role.

## Syntax

    
    
    atlas projects invitations invite <email> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
email

|

string

|

true

|

Email address that belongs to the user that you want to invite to the project.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
-h, --help

|

|

false

|

help for invite  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
\--role

|

strings

|

true

|

User's roles for the associated project. Valid values include
GROUP_CLUSTER_MANAGER, GROUP_DATA_ACCESS_ADMIN, GROUP_DATA_ACCESS_READ_ONLY,
GROUP_DATA_ACCESS_READ_WRITE, GROUP_OWNER, and GROUP_READ_ONLY.  
  
\--teamId

|

strings

|

false

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
  
## Examples

    
    
    # Invite the MongoDB user with the email user@example.com to the project with the ID 5f71e5255afec75a3d0f96dc with GROUP_READ_ONLY access:  
      
    atlas projects invitations invite user@example.com --projectId 5f71e5255afec75a3d0f96dc --role GROUP_READ_ONLY --output json  
  
What is MongoDB Atlas? →

