Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas config init

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Configure a profile to store access settings for your MongoDB deployment.

## Syntax

    
    
    atlas config init [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--gov

|

|

false

|

Create a default profile for atlas for gov  
  
-h, --help

|

|

false

|

help for init  
  
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

    
    
    # To configure the tool to work with Atlas:  
      
    atlas config init  
      
    
    # To configure the tool to work with Atlas for Government:  
      
    atlas config init --gov  
  
What is MongoDB Atlas? →

