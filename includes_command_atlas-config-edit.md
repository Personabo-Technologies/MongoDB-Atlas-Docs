Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas config edit

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Opens the config file with the default text editor.

Uses the default editor to open the config file. You can use EDITOR or VISUAL
envs to change the default.

## Syntax

    
    
    atlas config edit [options]  
      
  
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

help for edit  
  
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

    
    
    # To open the config  
      
    atlas config edit  
  
What is MongoDB Atlas? →

