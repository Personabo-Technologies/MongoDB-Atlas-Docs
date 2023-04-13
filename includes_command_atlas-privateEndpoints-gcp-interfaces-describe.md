Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints gcp interfaces describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return a specific GCP private endpoint interface for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas privateEndpoints gcp interfaces describe <id> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
id

|

string

|

true

|

Unique identifier of the private endpoint you want to retrieve.  
  
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

    
    
    atlas privateEndpoints gcp interfaces describe endpoint-1 \  
      
    --endpointServiceId 61eaca605af86411903de1dd  
  
What is MongoDB Atlas? →

