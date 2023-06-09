Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations apiKeys describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the specified API key for your organization.

To view possible values for the ID argument, run atlas organizations apiKeys
list.

To use this command, you must authenticate with a user account or an API key
that has the Organization Member role.

## Syntax

    
    
    atlas organizations apiKeys describe <ID> [options]  
      
  
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

Unique 24-digit string that identifies your API key.  
  
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
  
\--orgId

|

string

|

false

|

Organization ID to use. Overrides the settings in the configuration file or
environment variable.  
  
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

    
    
    # Return the JSON-formatted details for the organization API key with the ID 5f24084d8dbffa3ad3f21234 for the organization with the ID 5a1b39eec902201990f12345:  
      
    atlas organizations apiKeys describe 5f24084d8dbffa3ad3f21234 --orgId 5a1b39eec902201990f12345 -output json  
  
What is MongoDB Atlas? →

