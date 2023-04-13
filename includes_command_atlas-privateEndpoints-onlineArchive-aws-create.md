Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas privateEndpoints onlineArchive aws create

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output

Create a new Data Lake private endpoint for your project.

When you run this command: \- If the endpoint ID already exists and there is
no change to the associated comment, Atlas Data Lake makes no change to the
endpoint ID list. \- If the endpoint ID already exists and there is a change
to the associated comment, Atlas Data Lake updates the comment value only in
the endpoint ID list. \- If the endpoint ID doesn't exist, Atlas Data Lake
appends the new endpoint to the list of endpoints in the endpoint ID list.
Your API key must have the GROUP_ATLAS_ADMIN (Project Owner) role to create a
private endpoint.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas privateEndpoints onlineArchive aws create [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--comment

|

string

|

false

|

Optional description or comment for the entry.  
  
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
  
\--privateEndpointId

|

string

|

true

|

Unique 22-character alphanumeric string that identifies the AWS PrivateLink
connection in AWS. You can find this value on the AWS VPC Dashboard under
Endpoints > VPC ID.  
  
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

    
    
    Data Lake private endpoint '{{ (index .Results 0).EndpointID >' created.  
      
  
What is MongoDB Atlas? →

