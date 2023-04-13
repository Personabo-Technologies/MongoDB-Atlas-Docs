Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas security ldap get

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return the current LDAP configuration details for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas security ldap get [options]  
      
  
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

help for get  
  
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

    
    
    # Return the JSON-formatted details of the current LDAP configuration in the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas security ldap get --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

