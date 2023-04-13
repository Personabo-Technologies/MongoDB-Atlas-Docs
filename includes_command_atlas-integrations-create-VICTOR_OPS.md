Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas integrations create VICTOR_OPS

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create or update a Splunk On-Call integration for your project.

VictorOps is now Splunk On-Call.

The requesting API key must have the Organization Owner or Project Owner role
to configure an integration with Splunk On-Call.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas integrations create VICTOR_OPS [options]  
      
  
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

Splunk On-Call API key that allows Atlas to access your Splunk On-Call
account.  
  
-h, --help

|

|

false

|

help for VICTOR_OPS  
  
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
  
\--routingKey

|

string

|

true

|

Routing key associated with your Splunk On-Call account.  
  
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

    
    
    Victor Ops integration configured.  
      
  
## Examples

    
    
    # Integrate Splunk On-Call with Atlas using the routing key operations for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas integrations create VICTOR_OPS --apiKey a1a23bcdef45ghijk6789 --routingKey operations --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

