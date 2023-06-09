Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas alerts acknowledge

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Acknowledges the specified alert for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas alerts acknowledge <alertId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
alertId

|

string

|

true

|

ID of the alert you want to acknowledge or unacknowledge.  
  
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
  
-F, --forever

|

|

false

|

Acknowledges an alert 'forever'. You can't set both forever and until in the
same command.  
  
-h, --help

|

|

false

|

help for acknowledge  
  
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
  
\--until

|

string

|

false

|

ISO 8601-formatted time until which the alert has been acknowledged. This
command returns this value if a MongoDB user previously acknowledged this
alert. After this date, the alert becomes unacknowledged.  
  
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

    
    
    # Acknowledge an alert with the ID 5d1113b25a115342acc2d1aa in the project with the ID 5e2211c17a3e5a48f5497de3 until January 1 2028:  
      
    atlas alerts acknowledge 5d1113b25a115342acc2d1aa --until 2028-01-01T20:24:26Z --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

