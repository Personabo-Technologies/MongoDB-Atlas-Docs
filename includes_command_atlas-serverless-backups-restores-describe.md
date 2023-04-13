Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas serverless backups restores describe

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Describe a cloud backup restore job.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas serverless backups restores describe [options]  
      
  
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
  
\--restoreJobId

|

string

|

true

|

Unique identifier that identifies the Restore Job.  
  
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

    
    
    # Return the details for the continuous backup restore job with the ID 507f1f77bcf86cd799439011 for the serverless isntance named Cluster0:  
      
    atlas serverless backup restore describe --restoreJobId 507f1f77bcf86cd799439011 --clusterName Cluster0  
  
What is MongoDB Atlas? →

