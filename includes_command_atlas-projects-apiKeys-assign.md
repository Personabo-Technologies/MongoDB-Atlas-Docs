Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects apiKeys assign

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Assign the specified organization API key to your project and modify the API
key's roles for the project.

When you modify the roles for an organization API key with this command, the
values you specify overwrite the existing roles assigned to the API key.

To view possible values for the ID argument, run atlas organizations apiKeys
list.

## Syntax

    
    
    atlas projects apiKeys assign <ID> [options]  
      
  
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

Unique 24-digit string that identifies your API key.  
  
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

help for assign  
  
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

Role or roles that you want to assign to the API key. To assign more than one
role, you can specify each role with a separate role flag or specify all of
the roles as a comma-separated list using one role flag. Valid values are
GROUP_CLUSTER_MANAGER, GROUP_DATA_ACCESS_ADMIN, GROUP_DATA_ACCESS_READ_ONLY,
GROUP_DATA_ACCESS_READ_WRITE, GROUP_SEARCH_INDEX_EDITOR, GROUP_OWNER, and
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

    
    
    # Assign an organization API key with the ID 5f46ae53d58b421fe3edc115 and grant the GROUP_DATA_ACCESS_READ_WRITE role for the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas projects apiKeys assign 5f46ae53d58b421fe3edc115 --projectId 5e1234c17a3e5a48f5497de3 --role GROUP_DATA_ACCESS_READ_WRITE --output json  
  
What is MongoDB Atlas? →

