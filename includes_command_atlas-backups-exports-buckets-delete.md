Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups exports buckets delete

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Delete a snapshot export bucket.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas backups exports buckets delete [options]  
      
  
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
  
\--force

|

|

false

|

Flag that indicates whether to skip the confirmation prompt before proceeding
with the requested action.  
  
-h, --help

|

|

false

|

help for delete  
  
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

    
    
    Snapshot export bucket with id '<Name>' deleted.  
      
  
## Examples

    
    
    # The following deletes the continuous backup export bucket specified by ID:  
      
    atlas backup exports buckets delete --bucketId dbdb00ca12345678f901a234  
  
What is MongoDB Atlas? →

