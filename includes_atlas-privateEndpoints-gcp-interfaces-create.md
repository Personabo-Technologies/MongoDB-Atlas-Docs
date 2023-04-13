Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints gcp interfaces create

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Create a GCP private endpoint interface.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas privateEndpoints gcp interfaces create <endpointGroupId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
endpointGroupId

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
  
\--endpoint

|

strings

|

false

|

List of GCP endpoints in the group separated by commas, such as:
endpointName1@ipAddress1,...,endpointNameN@ipAddressN  
  
\--endpointServiceId

|

string

|

true

|

Unique 24-character alphanumeric string that identifies the private endpoint
in Atlas.  
  
\--gcpProjectId

|

string

|

true

|

Unique identifier of the GCP project in which the network peer resides.  
  
-h, --help

|

|

false

|

help for create  
  
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
  
## Output

If the command succeeds, the CLI returns output similar to the following
sample. Values in brackets represent your values.

    
    
    Interface endpoint '<EndpointGroupName>' created.  
      
  
## Examples

    
    
    atlas privateEndpoints gcp interfaces create endpoint-1 \  
      
    --endpointServiceId 61eaca605af86411903de1dd \  
    --gcpProjectId mcli-private-endpoints \  
    --endpoint endpoint-0@10.142.0.2,endpoint-1@10.142.0.3,endpoint-2@10.142.0.4,endpoint-3@10.142.0.5,endpoint-4@10.142.0.6,endpoint-5@10.142.0.7  
  
What is MongoDB Atlas? →

