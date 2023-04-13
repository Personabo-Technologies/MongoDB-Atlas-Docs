Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups snapshots create

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Create a backup snapshot for your project and cluster.

You can create on-demand backup snapshots for Atlas cluster tiers M10 and
larger.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas backups snapshots create <clusterName> [options]  
      
  
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

Name of the Atlas cluster whose snapshot you want to restore.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--desc

|

string

|

true

|

Description of the on-demand snapshot.  
  
-h, --help

|

|

false

|

help for create  
  
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
  
\--retention

|

int

|

false

|

Number of days that Atlas should retain the on-demand snapshot. Must be at
least 1. This value defaults to 1.  
  
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

    
    
    Snapshot '<ID>' created.  
      
  
## Examples

    
    
    # Create a backup snapshot for the cluster named myDemo that Atlas retains for 30 days:  
      
    atlas backups snapshots create myDemo --desc "test" --retention 30  
  
What is MongoDB Atlas? →

