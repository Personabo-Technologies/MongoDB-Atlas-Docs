Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas config list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return a list of available profiles by name.

If you did not specify a name for your profile, it displays as the default
profile.

## Syntax

    
    
    atlas config list [options]  
      
  
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
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
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

    
    
    atlas config ls  
      
  
What is MongoDB Atlas? →

