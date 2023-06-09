Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas integrations delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified third-party integration from your project.

Deleting an integration from a project removes that integration configuration
only for that project. This does not affect any other project or
organization's configured integrations.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas integrations delete <integrationType> [options]  
      
  
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

Human-readable label that identifies the service integration to delete. Valid
values are PAGER_DUTY, MICROSOFT_TEAMS, SLACK, DATADOG, NEW_RELIC, OPS_GENIE,
VICTOR_OPS, WEBHOOK, PROMETHEUS.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
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

    
    
    Integration '<Name>' deleted  
      
  
## Examples

    
    
    # Remove the Datadog integration for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas integrations delete DATADOG --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

