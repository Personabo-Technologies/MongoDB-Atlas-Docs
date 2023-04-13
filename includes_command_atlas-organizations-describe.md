Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the specified organizations.

To use this command, you must authenticate with a user account or an API key
that has the Organization Member role.

## Syntax

    
    
    atlas organizations describe <ID> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
ID

|

string

|

true

|

Unique 24-digit string that identifies the organization.  
  
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

help for describe  
  
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

    
    
    # Return the JSON-formatted details for the organization with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas organizations describe 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

