Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects apiKeys delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified organization API key from your project.

The API key still exists at the organization level. To reassign the
organization API key to a project, run the atlas projects apiKeys assign
command.

To view possible values for the ID argument, run atlas organizations apiKeys
list.

To use this command, you must authenticate with a user account or an API key
that has the Project User Admin role.

## Syntax

    
    
    atlas projects apiKeys delete <ID> [options]  
      
  
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

    
    
    API Key '<Name>' deleted  
      
  
## Examples

    
    
    # Remove an organization API key with the ID 5f46ae53d58b421fe3edc115 from the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas projects apiKeys delete 5f46ae53d58b421fe3edc115 --projectId 5e1234c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

