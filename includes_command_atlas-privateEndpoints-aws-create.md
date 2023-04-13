Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints aws create

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create a new AWS private endpoint for your project.

To learn more about how to set up private endpoints with the Atlas CLI, see
the tutorial on the Atlas CLI tab here:
https://www.mongodb.com/docs/atlas/security-cluster-private-endpoint/.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas privateEndpoints aws create [options]  
      
  
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

    
    
    Private endpoint '<ID>' created.  
      
  
## Examples

    
    
    # Create a private endpoint connection for AWS in the us-east-1 region for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas privateEndpoints aws create --region us-east-1 --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

