Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas serverless watch

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Monitor the status of serverless instance.

This command checks the serverless instance's state periodically until the
instance reaches an IDLE state. Once the instance reaches the expected state,
the command prints "Instance available." If you run the command in the
terminal, it blocks the terminal session until the resource becomes idle. You
can interrupt the command's polling at any time with CTRL-C.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas serverless watch <instanceName> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
instanceName

|

string

|

true

|

Name of the instance to watch.  
  
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

    
    
    atlas serverless watch instanceNameSample  
      
  
What is MongoDB Atlas? →

