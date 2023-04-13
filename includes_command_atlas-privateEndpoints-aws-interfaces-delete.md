Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints aws interfaces delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified AWS private endpoint interface and related service from
your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas privateEndpoints aws interfaces delete <interfaceEndpointId> [options]  
      
  
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

false

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

    
    
    # Remove the AWS private endpoint interface with the ID vpce-00713b5e644e830a3 in AWS from the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas privateEndpoints aws interfaces delete vpce-00713b5e644e830a3 --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

