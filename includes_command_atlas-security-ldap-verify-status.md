Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas security ldap verify status

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Related Commands

Get the status of an LDAP configuration request.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas security ldap verify status <requestId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
requestId

|

string

|

true

|

ID of the request to verify an LDAP configuration.  
  
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

help for status  
  
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
  
## Related Commands

  * atlas security ldap verify status watch \- Watch for an LDAP configuration request to complete.

What is MongoDB Atlas? →

