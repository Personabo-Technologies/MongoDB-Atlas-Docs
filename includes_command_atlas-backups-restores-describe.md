Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups restores describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Describe a cloud backup restore job.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas backups restores describe <restoreJobId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
restoreJobId

|

string

|

true

|

ID of the restore job.  
  
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

    
    
    # Return the details for the continuous backup restore job with the ID 507f1f77bcf86cd799439011 for the cluster named Cluster0:  
      
    atlas backup restore describe 507f1f77bcf86cd799439011 --clusterName Cluster0  
  
What is MongoDB Atlas? →

