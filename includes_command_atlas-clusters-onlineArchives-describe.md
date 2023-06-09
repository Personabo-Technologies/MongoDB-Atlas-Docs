Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters onlineArchives describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the specified online archive for your cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas clusters onlineArchives describe <archiveId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
archiveId

|

string

|

true

|

Unique identifier of the online archive to retrieve.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--clusterName

|

string

|

true

|

Name of the cluster.  
  
-h, --help

|

|

false

|

help for describe  
  
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

    
    
    # Return the JSON-formatted details for the online archive with the ID 5f189832e26ec075e10c32d3 for the cluster named myCluster:  
      
    atlas clusters onlineArchives describe 5f189832e26ec075e10c32d3 --clusterName myCluster --output json  
  
What is MongoDB Atlas? →

