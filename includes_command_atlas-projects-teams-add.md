Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects teams add

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Add the specified team to your project.

All members of the team share the same project access.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas projects teams add <teamId> [options]  
      
  
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
  
-h, --help

|

|

false

|

help for add  
  
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

User role that applies to all members of the specified team for the associated
project. Valid values include GROUP_CLUSTER_MANAGER, GROUP_DATA_ACCESS_ADMIN,
GROUP_DATA_ACCESS_READ_ONLY, GROUP_DATA_ACCESS_READ_WRITE, GROUP_OWNER, and
GROUP_READ_ONLY.  
  
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

    
    
    # Add the team with the ID 5dd58c647a3e5a6c5bce46c7 to the project with the ID 5e2211c17a3e5a48f5497de3 with GROUP_READ_ONLY project access:  
      
    atlas projects teams add 5dd58c647a3e5a6c5bce46c7 --projectId 5e2211c17a3e5a48f5497de3 --role GROUP_READ_ONLY  
  
What is MongoDB Atlas? →

