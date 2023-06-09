Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters search indexes describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the search index for a cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Data Access Read/Write role.

## Syntax

    
    
    atlas clusters search indexes describe <indexId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
indexId

|

string

|

true

|

ID of the index.  
  
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

    
    
    # Return the JSON-formatted details for the search index with the ID 5f1f40842f2ac35f49190c20 for the cluster named myCluster:  
      
    atlas clusters search indexes describe 5f1f40842f2ac35f49190c20 --clusterName myCluster --output json  
  
What is MongoDB Atlas? →

