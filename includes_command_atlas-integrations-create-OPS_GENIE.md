Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas integrations create OPS_GENIE

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create or update an Opsgenie integration for your project.

The requesting API key must have the Organization Owner or Project Owner role
to configure an integration with Opsgenie.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas integrations create OPS_GENIE [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--apiKey

|

string

|

true

|

Opsgenie API key that allows Atlas to access your Opsgenie account.  
  
-h, --help

|

|

false

|

help for OPS_GENIE  
  
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

false

|

Code that indicates which regional URL MongoDB uses to access the third-party
API. Valid values are US and EU. This value defaults to "US".  
  
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

    
    
    Ops Genie integration configured.  
      
  
## Examples

    
    
    # Integrate Opsgenie with Atlas for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas integrations create OPS_GENIE --apiKey a1a23bcdef45ghijk6789 --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

