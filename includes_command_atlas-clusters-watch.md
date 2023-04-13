Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters watch

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Watch the specified cluster in your project until it becomes available.

This command checks the cluster's status periodically until it reaches an IDLE
state. Once the cluster reaches the expected state, the command prints
"Cluster available." If you run the command in the terminal, it blocks the
terminal session until the resource state changes to IDLE. You can interrupt
the command's polling at any time with CTRL-C.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas clusters watch <clusterName> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
clusterName

|

string

|

true

|

Name of the cluster to watch.  
  
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

    
    
    # Watch for the cluster named myCluster to become available for the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas clusters watch myCluster --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

