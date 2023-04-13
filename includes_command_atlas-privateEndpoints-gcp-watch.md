Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints gcp watch

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Watch the specified GCP private endpoint to detect changes in the endpoint's
state.

This command checks the endpoint's state periodically until the endpoint
reaches an AVAILABLE or FAILED state. Once the endpoint reaches the expected
state, the command prints "GCP Private endpoint changes completed." If you run
the command in the terminal, it blocks the terminal session until the resource
becomes available or fails. You can interrupt the command's polling at any
time with CTRL-C.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas privateEndpoints gcp watch <privateEndpointId> [options]  
      
  
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
  
-h, --help

|

|

false

|

help for watch  
  
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

    
    
    atlas privateEndpoint gcp watch vpce-abcdefg0123456789  
      
  
What is MongoDB Atlas? →

