Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas networking peering watch

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Watch the specified peering connection in your project until it becomes
available.

This command checks the peering connection's status periodically until it
becomes available. Once it reaches the expected state, the command prints
"Network peering changes completed." If you run the command in the terminal,
it blocks the terminal session until the resource is available. You can
interrupt the command's polling at any time with CTRL-C.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas networking peering watch <peerId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
peerId

|

string

|

true

|

Unique ID of the network peering connection that you want to watch.  
  
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

    
    
    Watch for the network peering connection with the ID 5f621dc701240c5b7c3a888e to become available in the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas networking peering watch 5f621dc701240c5b7c3a888e --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

