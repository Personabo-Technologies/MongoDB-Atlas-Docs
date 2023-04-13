Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas config rename

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Rename a profile.

## Syntax

    
    
    atlas config rename <oldProfileName> <newProfileName> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
oldProfileName

|

string

|

true

|

Name of the profile to rename.  
  
newProfileName

|

string

|

true

|

New name of the profile.  
  
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

help for rename  
  
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

    
    
    # Rename a profile called myProfile to testProfile:  
      
    atlas config rename myProfile testProfile  
  
What is MongoDB Atlas? →

