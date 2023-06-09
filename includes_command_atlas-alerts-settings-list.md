Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas alerts settings list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Returns all alert configurations for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas alerts settings list [options]  
      
  
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
  
\--limit

|

int

|

false

|

Number of items per results page.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--page

|

int

|

false

|

Page number that specifies a page of results.  
  
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

    
    
    # Return a JSON-formatted list of all alert configurations for the project with the ID 5df90590f10fab5e33de2305:  
      
    atlas alerts settings list --projectId 5df90590f10fab5e33de2305 --output json  
  
What is MongoDB Atlas? →

