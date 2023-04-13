Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas customDbRoles describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options

Return a single custom database role for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas customDbRoles describe <roleName> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
roleName

|

string

|

true

|

Name of the custom role to retrieve.  
  
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

help for describe  
  
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
  
What is MongoDB Atlas? →

