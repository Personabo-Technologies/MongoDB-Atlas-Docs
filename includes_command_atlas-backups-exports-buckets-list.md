Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups exports buckets list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

List cloud backup restore buckets for your project and cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas backups exports buckets list [options]  
      
  
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

    
    
    # Return all continuous backup export buckets for your project:  
      
    atlas backup exports buckets list  
  
What is MongoDB Atlas? →

