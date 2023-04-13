Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas maintenanceWindows update

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Modify the maintenance window for your project.

To learn more about maintenance windows, see
https://www.mongodb.com/docs/atlas/tutorial/cluster-maintenance-window/.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas maintenanceWindows update [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--dayOfWeek

|

int

|

false

|

Day of the week that you want the maintenance window to start, as a 1-based
integer. Use 1 for Sunday, 2 for Monday, 3 for Tuesday, 4 for Wednesday, 5 for
Thursday, 6 for Friday, or 7 for Saturday.  
  
-h, --help

|

|

false

|

help for update  
  
\--hourOfDay

|

int

|

false

|

Hour of the day that you want the maintenance window to start according to a
24-hour clock. Use 0 for midnight and 12 for noon.  
  
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
  
\--startASAP

|

|

false

|

Flag that starts maintenance immediately upon receiving this request. This
flag resets to false after Atlas completes maintenance.  
  
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

    
    
    Maintenance window updated.  
      
  
## Examples

    
    
    # Update the maintenance window to midnight on Saturdays for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas maintenanceWindows update --dayOfWeek 7 --hourOfDay 0 --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

