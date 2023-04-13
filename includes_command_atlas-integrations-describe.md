Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas integrations describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the specified third-party integration for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas integrations describe <integrationType> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
integrationType

|

string

|

true

|

Human-readable label that identifies the integrated service. Valid values are
PAGER_DUTY, MICROSOFT_TEAMS, SLACK, DATADOG, NEW_RELIC, OPS_GENIE, VICTOR_OPS,
WEBHOOK, PROMETHEUS.  
  
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

help for describe  
  
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
  
## Examples

    
    
    # Return the JSON-formatted details for the Datadog integration for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas integrations describe DATADOG --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

