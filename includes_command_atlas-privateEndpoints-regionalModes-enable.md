Docs Home → MongoDB Atlas

# atlas privateEndpoints regionalModes enable

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Enable the regionalized private endpoint setting for your project.

This enables the ability to create multiple private resources per region in
all cloud service providers for this project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas privateEndpoints regionalModes enable [options]  
      
  
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

help for enable  
  
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

    
    
    # Enable the regionalied private endpoint setting in the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas privateEndpoints regionalModes enable --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

