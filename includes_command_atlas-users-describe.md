Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas users describe

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return the details for the specified MongoDB user.

You can specify either the unique 24-digit ID that identifies the MongoDB user
or the username for the MongoDB user.

User accounts and API keys with any role can run this command.

## Syntax

    
    
    atlas users describe [options]  
      
  
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
  
\--id

|

string

|

false

|

Unique 24-digit identifier of the user.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--username

|

string

|

false

|

Username that identifies the user. This value must be a valid email address.  
  
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

    
    
    # Return the JSON-formatted details for the MongoDB user with the ID 5dd56c847a3e5a1f363d424d:  
      
    atlas users describe --id 5dd56c847a3e5a1f363d424d --output json  
      
    
    # Return the JSON-formatted details for the MongoDB user with the username myUser:  
      
    atlas users describe --username myUser --output json  
  
What is MongoDB Atlas? →

