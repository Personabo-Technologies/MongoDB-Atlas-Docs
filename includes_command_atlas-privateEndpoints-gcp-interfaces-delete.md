Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints gcp interfaces delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Delete a specific GCP private endpoint interface for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas privateEndpoints gcp interfaces delete <id> [options]  
      
  
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

Unique identifier for the endpoint group.  
  
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
  
\--force

|

|

false

|

Flag that indicates whether to skip the confirmation prompt before proceeding
with the requested action.  
  
-h, --help

|

|

false

|

help for delete  
  
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
  
## Output

If the command succeeds, the CLI returns output similar to the following
sample. Values in brackets represent your values.

    
    
    Interface endpoint '<Name>' deleted  
      
  
## Examples

    
    
    atlas privateEndpoints gcp interfaces delete endpoint-1 \  
      
    --endpointServiceId 61eaca605af86411903de1dd  
  
What is MongoDB Atlas? →

