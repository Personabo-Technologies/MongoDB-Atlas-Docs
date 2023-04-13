Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas maintenanceWindows describe

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return the maintenance window details for your project.

To learn more about maintenance windows, see
https://www.mongodb.com/docs/atlas/tutorial/cluster-maintenance-window/.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas maintenanceWindows describe [options]  
      
  
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
  
## Examples

    
    
    # Return the maintenance window for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas maintenanceWindows describe --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

