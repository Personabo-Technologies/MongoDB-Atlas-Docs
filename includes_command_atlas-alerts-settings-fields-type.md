Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas alerts settings fields type

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return all available field types that the matcherFieldName option accepts when
you create or update an alert configuration.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas alerts settings fields type [options]  
      
  
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

help for type  
  
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

    
    
    # Return a JSON-formatted list of accepted field types for the matchersFieldName option:  
      
    atlas alerts settings fields type --output json  
  
What is MongoDB Atlas? →

