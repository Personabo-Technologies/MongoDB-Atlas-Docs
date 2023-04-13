Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas integrations create WEBHOOK

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create or update a webhook integration for your project.

The requesting API key must have the Organization Owner or Project Owner role
to configure a webhook integration.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas integrations create WEBHOOK [options]  
      
  
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

help for WEBHOOK  
  
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
  
\--secret

|

string

|

true

|

Secret that secures your webhook.  
  
\--url

|

string

|

true

|

Endpoint web address to which Atlas sends notifications.  
  
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

    
    
    Webhook integration configured.  
      
  
## Examples

    
    
    # Integrate a webhook with Atlas that uses the secret mySecret for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas integrations create WEBHOOK --url http://9b4ac7aa.abc.io/payload --secret mySecret --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

