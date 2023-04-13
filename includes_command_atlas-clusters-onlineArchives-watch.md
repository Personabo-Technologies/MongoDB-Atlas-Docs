Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters onlineArchives watch

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Watch for an archive to be available.

This command checks the archive's status periodically until it reaches a state
different from PENDING or PAUSING. Once the archive reaches the expected
status, the command prints "Online archive available." If you run the command
in the terminal, it blocks the terminal session until the resource status
changes to the expected status. You can interrupt the command's polling at any
time with CTRL-C.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas clusters onlineArchives watch <archiveId> [options]  
      
  
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

Unique identifier of the online archive to watch.  
  
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

false

|

Name of the cluster.  
  
-h, --help

|

|

false

|

help for watch  
  
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

    
    
    atlas cluster onlineArchive watch archiveIdSample --clusterName clusterNameSample  
      
  
What is MongoDB Atlas? →

