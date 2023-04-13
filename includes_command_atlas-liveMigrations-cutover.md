Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas liveMigrations cutover

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options

Start the cutover for a push live migration and confirm when the cutover
completes. When the cutover completes, the application completes the live
migration process and stops synchronizing with the source cluster.

To migrate using scripts, use mongomirror instead of the Atlas CLI. To learn
more about mongomirror, see
https://www.mongodb.com/docs/atlas/reference/mongomirror/.

## Syntax

    
    
    atlas liveMigrations cutover [options]  
      
  
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

help for cutover  
  
\--liveMigrationId

|

string

|

true

|

Unique 24-hexadecimal digit string that identifies the live migration job.  
  
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
  
What is MongoDB Atlas? →

