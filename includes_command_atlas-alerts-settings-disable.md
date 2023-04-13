Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas alerts settings disable

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options

Disables one alert configuration for the specified project.

## Syntax

    
    
    atlas alerts settings disable <alertConfigId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
alertConfigId

|

string

|

true

|

ID of the alert configuration you want to disable.  
  
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

help for disable  
  
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
