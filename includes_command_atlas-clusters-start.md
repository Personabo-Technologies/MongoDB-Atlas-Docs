Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters start

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Start the specified paused MongoDB cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Cluster Manager role.

## Syntax

    
    
    atlas clusters start <clusterName> [options]  
      
  
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

Name of the cluster to start.  
  
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

help for start  
  
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

    
    
    # Start a cluster named myCluster for the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas clusters start myCluster --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

