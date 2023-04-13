Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas alerts list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return all alerts for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas alerts list [options]  
      
  
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
  
\--status

|

string

|

false

|

State of this alert. Valid values are TRACKING, OPEN, CLOSED, and CANCELLED.  
  
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

    
    
    # Return a JSON-formatted list of all alerts for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas alerts list --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

