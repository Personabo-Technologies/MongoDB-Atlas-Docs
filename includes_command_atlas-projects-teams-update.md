Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects teams update

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Modify the roles for the specified team for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project User Admin role.

## Syntax

    
    
    atlas projects teams update <teamId> [options]  
      
  
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

help for update  
  
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
  
## Output

If the command succeeds, the CLI returns output similar to the following
sample. Values in brackets represent your values.

    
    
    Team's roles updated.  
      
  
## Examples

    
    
    # Modify the roles for the team with the ID 5dd56c847a3e5a1f363d424d to grant GROUP_READ_ONLY access to the project with the ID 5f71e5255afec75a3d0f96dc:  
      
    atlas projects teams update 5dd56c847a3e5a1f363d424d --projectId 5f71e5255afec75a3d0f96dc --role GROUP_READ_ONLY --output json  
  
What is MongoDB Atlas? →

