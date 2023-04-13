Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints gcp delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Delete a GCP private endpoint for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas privateEndpoints gcp delete <privateEndpointId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
privateEndpointId

|

string

|

true

|

Unique 22-character alphanumeric string that identifies the private endpoint.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
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

    
    
    Private endpoint '<Name>' deleted  
      
  
## Examples

    
    
    atlas privateEndpoint gcp delete vpce-abcdefg0123456789 --force  
      
  
What is MongoDB Atlas? →

