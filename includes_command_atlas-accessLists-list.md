Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas accessLists list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return all IP access list entries for your project.

To use this command, you must authenticate with a user account or an API key
that has the Organization Member role.

## Syntax

    
    
    atlas accessLists list [options]  
      
  
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

Number of items per results page. This value defaults to 100.  
  
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

Page number that specifies a page of results. This value defaults to 1.  
  
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

    
    
    # Return a JSON-formatted list of all access list entries for the project with ID 5e1234c17a3e5a48f5497de3:  
      
    atlas accessLists list --output json --projectId 5e1234c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

