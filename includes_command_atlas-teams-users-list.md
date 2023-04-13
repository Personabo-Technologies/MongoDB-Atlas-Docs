Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas teams users list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return all users for a team.

To use this command, you must authenticate with a user account or an API key
that has the Organization Member role.

## Syntax

    
    
    atlas teams users list [options]  
      
  
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

help for list  
  
\--orgId

|

string

|

false

|

Organization ID to use. Overrides the settings in the configuration file or
environment variable.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
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
  
## Examples

    
    
    # Return a JSON-formatted list of the users for the team with the ID 5f6a5c6c713184005d72fe6e in the organization with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas teams users list --teamId 5f6a5c6c713184005d72fe6e --orgId 5e1234c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

