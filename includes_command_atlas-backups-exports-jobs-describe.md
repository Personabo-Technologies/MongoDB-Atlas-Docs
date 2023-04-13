Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups exports jobs describe

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return one cloud backup export job for your project, cluster and job.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas backups exports jobs describe [options]  
      
  
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
  
\--exportId

|

string

|

false

|

Unique string that identifies the AWS S3 bucket to which you export your
snapshots.  
  
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

    
    
    # Return the details for the continuous backup export job with the ID 5df90590f10fab5e33de2305 for the cluster named Cluster0:  
      
    atlas backup exports jobs describe --clusterName Cluster0 --exportID 5df90590f10fab5e33de2305  
  
What is MongoDB Atlas? →

