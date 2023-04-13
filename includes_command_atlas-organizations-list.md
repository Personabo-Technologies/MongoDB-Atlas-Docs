Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return all organizations.

To use this command, you must authenticate with a user account or an API key
that has the Organization Member role.

## Syntax

    
    
    atlas organizations list [options]  
      
  
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
  
\--includeDeleted

|

|

false

|

If specified, includes deleted organizations in the list. This option applies
only to Ops Manager organizations. You can't return deleted Atlas or Cloud
Manager organizations.  
  
\--limit

|

int

|

false

|

Number of items per results page. This value defaults to 100.  
  
\--name

|

string

|

false

|

Performs a case-insensitive search for organizations that exactly match the
specified organization name.  
  
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

    
    
    # Return a JSON-formatted list of all organizations:  
      
    atlas organizations list --output json  
      
    
    # Return a JSON-formatted list that includes the organizations named org1 and Org1, but doesn't return org123:  
      
    atlas organizations list --name org1 --output json  
  
What is MongoDB Atlas? →

