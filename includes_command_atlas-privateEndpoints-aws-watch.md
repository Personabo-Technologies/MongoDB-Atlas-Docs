Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints aws watch

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Watch the specified AWS private endpoint in your project until it becomes
available.

This command checks the endpoint's state periodically until the endpoint
reaches an AVAILABLE or FAILED state. Once the endpoint reaches the expected
state, the command prints "Private endpoint changes completed." If you run the
command in the terminal, it blocks the terminal session until the resource
becomes available or fails. You can interrupt the command's polling at any
time with CTRL-C.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas privateEndpoints aws watch <privateEndpointId> [options]  
      
  
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

Unique 24-character alphanumeric string that identifies the private endpoint
in Atlas.  
  
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

    
    
    # Watch for the AWS private endpoint with the ID 5f4fc14da2b47835a58c63a2 to become available in the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas privateEndpoints aws watch 5f4fc14da2b47835a58c63a2 --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

