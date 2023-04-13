Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups schedule describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Describe a cloud backup schedule for the cluster you specify.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas backups schedule describe <clusterName> [options]  
      
  
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

Human-readable label for the cluster.  
  
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

    
    
    # Return the cloud backup schedule for the cluster named Cluster0:  
      
    atlas backup schedule describe Cluster0  
  
What is MongoDB Atlas? →

