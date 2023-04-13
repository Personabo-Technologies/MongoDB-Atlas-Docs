Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas accessLists describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the specified IP access list entry.

To use this command, you must authenticate with a user account or an API key
that has the Organization Member role.

## Syntax

    
    
    atlas accessLists describe <entry> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
entry

|

string

|

true

|

The IP address, CIDR address, or AWS security group ID of the access list
entry to return.  
  
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

    
    
    # Return the JSON-formatted details for the access list entry 192.0.2.0/24 in the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas accessLists describe 192.0.2.0/24 --output json --projectId 5e1234c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

