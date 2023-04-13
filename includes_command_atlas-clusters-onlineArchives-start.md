Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters onlineArchives start

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options

Start a paused online archive from a cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Data Access Admin role.

## Syntax

    
    
    atlas clusters onlineArchives start <archiveId> [options]  
      
  
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

Unique identifier of the online archive to start.  
  
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
  
What is MongoDB Atlas? →

