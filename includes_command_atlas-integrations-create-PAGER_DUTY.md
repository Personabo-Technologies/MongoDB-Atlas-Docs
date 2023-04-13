Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas integrations create PAGER_DUTY

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create or update a PagerDuty integration for your project.

The requesting API key must have the Organization Owner or Project Owner role
to configure an integration with PagerDuty.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas integrations create PAGER_DUTY [options]  
      
  
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

help for PAGER_DUTY  
  
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
  
\--serviceKey

|

string

|

true

|

Service key associated with your PagerDuty account.  
  
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

    
    
    Pager Duty integration configured.  
      
  
## Examples

    
    
    # Integrate PagerDuty with Atlas for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas integrations create PAGER_DUTY --serviceKey a1a23bcdef45ghijk6789 --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

