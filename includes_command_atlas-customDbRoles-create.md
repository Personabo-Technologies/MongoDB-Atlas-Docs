Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas customDbRoles create

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Create a custom database role for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas customDbRoles create <roleName> [options]  
      
  
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

Name of the custom role to create.  
  
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

help for create  
  
\--inheritedRole

|

strings

|

false

|

List of inherited roles and the database on which the role is granted.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--privilege

|

strings

|

false

|

List of actions per database and collection. If no database or collections are
provided, cluster scope is assumed.  
  
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

    
    
    Custom database role '<RoleName>' successfully created.  
      
  
## Examples

    
    
    atlas customDbRoles create customRole --privilege FIND@database,UPDATE@database  
      
  
What is MongoDB Atlas? →

