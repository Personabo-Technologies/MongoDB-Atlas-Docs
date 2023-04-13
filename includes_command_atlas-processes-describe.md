Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas processes describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the specified MongoDB process for your project.

## Syntax

    
    
    atlas processes describe <hostname:port> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
hostname:port

|

string

|

true

|

Hostname and port number of the instance running the Atlas MongoDB process.  
  
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

    
    
    # Return the JSON-formatted details for the MongoDB process with hostname and port atlas-lnmtkm-shard-00-00.ajlj3.mongodb.net:27017  
      
    atlas process describe atlas-lnmtkm-shard-00-00.ajlj3.mongodb.net:27017 --output json  
  
What is MongoDB Atlas? →

