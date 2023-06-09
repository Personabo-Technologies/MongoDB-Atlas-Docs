Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas security ldap verify status watch

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Watch for an LDAP configuration request to complete.

This command checks the LDAP configuration's status periodically until it
reaches a SUCCESS or FAILED status. Once the LDAP configuration reaches the
expected status, the command prints "LDAP Configuration request completed." If
you run the command in the terminal, it blocks the terminal session until the
resource status succeeds or fails. You can interrupt the command's polling at
any time with CTRL-C.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas security ldap verify status watch <requestId> [options]  
      
  
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

help for watch  
  
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

    
    
    atlas security ldap status watch requestIdSample  
      
  
What is MongoDB Atlas? →

