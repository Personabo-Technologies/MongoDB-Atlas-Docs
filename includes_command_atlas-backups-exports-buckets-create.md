Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas backups exports buckets create

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Create an export destination for Atlas backups using an existing AWS S3
bucket.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas backups exports buckets create <bucketName> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
bucketName

|

string

|

true

|

Name of the existing S3 bucket that the provided role ID is authorized to
access.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--cloudProvider

|

string

|

true

|

Name of the provider of the cloud service where Atlas can access the S3
bucket. Atlas only supports AWS.  
  
-h, --help

|

|

false

|

help for create  
  
\--iamRoleId

|

string

|

true

|

Unique identifier that Atlas assigns to the the cloud provider access role for
the bucket.  
  
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

    
    
    Export destination created using '<BucketName>'.  
      
  
## Examples

    
    
    # The following command creates an export destination for Atlas backups using the existing AWS S3 bucket named test-bucket:  
      
    atlas backup export buckets create test-bucket --cloudProvider AWS --iamRoleId 12345678f901a234dbdb00ca  
  
What is MongoDB Atlas? →

