Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas auth login

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Authenticate with MongoDB Atlas.

## Syntax

    
    
    atlas auth login [options]  
      
  
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

Log in to Atlas for Government.  
  
-h, --help

|

|

false

|

help for login  
  
\--noBrowser

|

|

false

|

Don't try to open a browser session.  
  
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

    
    
    # To start the interactive login for your MongoDB Atlas account:  
      
    atlas auth login  
  
What is MongoDB Atlas? →

