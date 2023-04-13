Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects settings update

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Updates settings for a project.

## Syntax

    
    
    atlas projects settings update [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--disableCollectDatabaseSpecificsStatistics

|

|

false

|

Flag that disables the Collect Database Specific Statistics project setting.  
  
\--disableDataExplorer

|

|

false

|

Flag that disables the Data Explorer project setting.  
  
\--disablePerformanceAdvisor

|

|

false

|

Flag that disables the Performance Advisor project setting.  
  
\--disableRealtimePerformancePanel

|

|

false

|

Flag that disables the Real Time Performance Panel project setting.  
  
\--disableSchemaAdvisor

|

|

false

|

Flag that disables the Schema Advisor project setting.  
  
\--enableCollectDatabaseSpecificsStatistics

|

|

false

|

Flag that enables the Collect Database Specific Statistics project setting.  
  
\--enableDataExplorer

|

|

false

|

Flag that enables the Data Explorer project setting.  
  
\--enablePerformanceAdvisor

|

|

false

|

Flag that enables the Performance Advisor project setting.  
  
\--enableRealtimePerformancePanel

|

|

false

|

Flag that enables the Real Time Performance Panel project setting.  
  
\--enableSchemaAdvisor

|

|

false

|

Flag that enables the Schema Advisor project setting.  
  
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

    
    
    Project settings updated.  
      
  
## Examples

    
    
    # This example uses the profile named "myprofile" for accessing Atlas.  
      
    atlas projects settings update --disableCollectDatabaseSpecificsStatistics -P myprofile  
  
What is MongoDB Atlas? →

