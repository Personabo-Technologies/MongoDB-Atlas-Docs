Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters onlineArchives update

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Modify the archiving rule for the specified online archive for a cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Data Access Admin role.

## Syntax

    
    
    atlas clusters onlineArchives update <archiveId> [options]  
      
  
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

Unique identifier of the online archive to update.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--archiveAfter

|

float

|

true

|

Number of days after which to archive cluster data.  
  
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

help for update  
  
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
  
## Output

If the command succeeds, the CLI returns output similar to the following
sample. Values in brackets represent your values.

    
    
    Online archive '<ID>' updated.  
      
  
## Examples

    
    
    # Update the archiving rule to archive after 5 days for the online archive with the ID 5f189832e26ec075e10c32d3 for the cluster named myCluster:  
      
    atlas clusters onlineArchives update 5f189832e26ec075e10c32d3 --clusterName --archiveAfter 5 myCluster --output json  
  
What is MongoDB Atlas? →

