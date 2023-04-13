Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters failover

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Starts a failover test for the specified cluster in the specified project.

Clusters contain a group of hosts that maintain the same data set. A failover
test checks how MongoDB Cloud handles the failure of the cluster's primary
node. During the test, MongoDB Cloud shuts down the primary node and elects a
new primary.

## Syntax

    
    
    atlas clusters failover <clusterName> [options]  
      
  
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

Human-readable label that identifies the cluster to start a failover test for.  
  
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

help for failover  
  
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

    
    
    # Test failover for a cluster named myCluster:  
      
    atlas clusters failover myCluster  
  
What is MongoDB Atlas? →

