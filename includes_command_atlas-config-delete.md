Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas config delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Delete a profile.

## Syntax

    
    
    atlas config delete <name> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
name

|

string

|

true

|

Name of the profile.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--force

|

|

false

|

Flag that indicates whether to skip the confirmation prompt before proceeding
with the requested action.  
  
-h, --help

|

|

false

|

help for delete  
  
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

    
    
    Profile '<Name>' deleted  
      
  
## Examples

    
    
    # Delete the default profile configuration:  
      
    atlas config delete default  
      
    
    # Skip the confirmation question and delete the default profile configuration:  
      
    atlas config delete default --force  
  
What is MongoDB Atlas? →

