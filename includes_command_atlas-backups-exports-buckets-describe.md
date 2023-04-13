Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups exports buckets describe

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return one snapshot export bucket.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas backups exports buckets describe [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--bucketId

|

string

|

true

|

Unique identifier that Atlas assigns to the bucket.  
  
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

    
    
    # Return the details for the continuous backup export bucket with the ID dbdb00ca12345678f901a234:  
      
    atlas backup exports buckets describe dbdb00ca12345678f901a234  
  
What is MongoDB Atlas? →

