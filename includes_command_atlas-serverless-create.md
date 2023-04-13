Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas serverless create

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output

Creates one serverless instance in the specified project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas serverless create <instanceName> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
instanceName

|

string

|

true

|

Human-readable label that identifies your serverless instance.  
  
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
  
\--provider

|

string

|

true

|

Cloud service provider that applies to the provisioned serverless instance.  
  
\--region

|

string

|

true

|

Human-readable label that identifies the physical location of your MongoDB
serverless instance. The region you choose can affect network latency for
clients accessing your databases.  
  
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

    
    
    Serverless instance <Name> created.  
      
  
What is MongoDB Atlas? →

