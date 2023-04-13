Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas serverless backups restores watch

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Watch the specified backup restore job until it completes.

This command checks the restore job's status periodically until it reaches a
completed, failed or canceled status. Command finishes once one of the
expected statuses are reached. If you run the command in the terminal, it
blocks the terminal session until the resource status completes or fails. You
can interrupt the command's polling at any time with CTRL-C. To use this
command, you must authenticate with a user account or an API key that has the
Project Read Only role.

## Syntax

    
    
    atlas serverless backups restores watch [options]  
      
  
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

    
    
    # Watch the continuous backup restore job with the ID 507f1f77bcf86cd799439011 for the cluster named Cluster0 until it becomes available:  
      
    atlas serverless backup restore watch --restoreJobId 507f1f77bcf86cd799439011 --clusterName Cluster0  
  
What is MongoDB Atlas? →

