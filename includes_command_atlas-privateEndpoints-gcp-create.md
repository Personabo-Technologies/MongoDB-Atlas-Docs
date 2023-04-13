Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints gcp create

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create a new GCP private endpoint for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas privateEndpoints gcp create [options]  
      
  
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
  
\--region

|

string

|

true

|

Cloud provider region in which you want to create the private endpoint
connection. For a complete list of supported AWS regions, see:
https://www.mongodb.com/docs/atlas/reference/amazon-aws/. For a complete list
of supported Azure regions, see:
https://www.mongodb.com/docs/atlas/reference/microsoft-azure/#microsoft-azure.
For a complete list of supported GCP regions, see:
https://www.mongodb.com/docs/atlas/reference/google-gcp/.  
  
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

    
    
    GCP private endpoint '<ID>' created.  
      
  
## Examples

    
    
    atlas privateEndpoints gcp create --region CENTRAL_US  
      
  
What is MongoDB Atlas? →

