Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas metrics disks list

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return all disks or disk partitions on the specified host for your project.

To return the hostname and port needed for this command, run: $ atlas
processes list

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas metrics disks list <hostname:port> [options]  
      
  
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

Hostname and port number of the instance running the MongoDB process.  
  
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

help for list  
  
\--limit

|

int

|

false

|

Number of items per results page. This value defaults to 100.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--page

|

int

|

false

|

Page number that specifies a page of results. This value defaults to 1.  
  
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

    
    
    # Return a JSON-formatted list of disks and partitions for the host atlas-lnmtkm-shard-00-00.ajlj3.mongodb.net:27017  
      
    atlas metrics disks list atlas-lnmtkm-shard-00-00.ajlj3.mongodb.net:27017 --output json  
  
What is MongoDB Atlas? →

