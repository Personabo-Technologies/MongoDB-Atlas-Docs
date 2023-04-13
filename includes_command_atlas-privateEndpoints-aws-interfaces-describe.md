Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints aws interfaces describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the specified AWS private endpoint interface for your
project.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas privateEndpoints aws interfaces describe <interfaceEndpointId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
interfaceEndpointId

|

string

|

true

|

Unique string that identifies the AWS private endpoint interface in AWS.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--endpointServiceId

|

string

|

true

|

Unique 24-character alphanumeric string that identifies the private endpoint
in Atlas.  
  
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

    
    
    # Return the JSON-formatted details of the AWS private endpoint interface with the ID  
      
                 vpce-00713b5e644e830a3 in AWS for an AWS private endpoint with the ID 5f4fc14da2b47835a58c63a2 in Atlas:  
    atlas privateEndpoints aws interfaces describe  
    vpce-00713b5e644e830a3 --endpointServiceId 5f4fc14da2b47835a58c63a2  
  
What is MongoDB Atlas? →

