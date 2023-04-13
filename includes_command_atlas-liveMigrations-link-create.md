Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas liveMigrations link create

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output

Create a new link-token for a push live migration.

To migrate using scripts, use mongomirror instead of the Atlas CLI. To learn
more about mongomirror, see
https://www.mongodb.com/docs/atlas/reference/mongomirror/.

## Syntax

    
    
    atlas liveMigrations link create [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--accessListIp

|

strings

|

false

|

IP address access list entries that are associated with the link-token.  
  
-h, --help

|

|

false

|

help for create  
  
\--orgId

|

string

|

false

|

Organization ID to use. Overrides the settings in the configuration file or
environment variable.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
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

    
    
    Link-token '<LinkToken>' successfully created.  
      
  
What is MongoDB Atlas? →

