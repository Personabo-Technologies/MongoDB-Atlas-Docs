Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects invitations list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return all pending invitations to your project.

To use this command, you must authenticate with a user account or an API key
that has the Project User Admin role.

## Syntax

    
    
    atlas projects invitations list [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--email

|

string

|

false

|

Email address for the user.  
  
-h, --help

|

|

false

|

help for list  
  
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

    
    
    # Return a JSON-formatted list of pending invitations to the project with the ID 5f71e5255afec75a3d0f96dc:  
      
    atlas projects invitations list --projectId 5f71e5255afec75a3d0f96dc --output json  
  
What is MongoDB Atlas? →

