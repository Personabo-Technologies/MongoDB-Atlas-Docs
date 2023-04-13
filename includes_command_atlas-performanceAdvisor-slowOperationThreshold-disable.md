Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas performanceAdvisor slowOperationThreshold disable

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options

Disable the application-managed slow operation threshold for your project.

The slow operation threshold determines which operations are flagged by the
Performance Advisor and Query Profiler. When disabled, the application
considers any operation that takes longer than 100 milliseconds to be slow.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas performanceAdvisor slowOperationThreshold disable [options]  
      
  
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

help for disable  
  
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

