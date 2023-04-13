Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters pause

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Pause the specified running MongoDB cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Cluster Manager role.

## Syntax

    
    
    atlas clusters pause <clusterName> [options]  
      
  
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

Name of the cluster to pause.  
  
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

help for pause  
  
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

    
    
    # Pause the cluster named myCluster for the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas clusters pause myCluster --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

