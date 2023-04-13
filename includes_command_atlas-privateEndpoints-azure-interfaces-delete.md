Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints azure interfaces delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified Azure private endpoint interface and related service from
your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas privateEndpoints azure interfaces delete <privateEndpointResourceId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
privateEndpointResourceId

|

string

|

true

|

Unique string that identifies the Azure private endpoint interface in Azure.  
  
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

    
    
    # Remove the Azure private endpoint interface with the ID /subscriptions/4e133d35-e734-4385-a565-c0945567ae346/resourceGroups/rg_95847a959b876e255dbb9b33_dfragd7w/providers/Microsoft.Network/privateEndpoints/cli-test in Azure from the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas privateEndpoints azure interfaces delete /subscriptions/4e133d35-e734-4385-a565-c0945567ae346/resourceGroups/rg_95847a959b876e255dbb9b33_dfragd7w/providers/Microsoft.Network/privateEndpoints/cli-test --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

