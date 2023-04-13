Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations apiKeys accessLists delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified IP access list entry from your API Key.

To use this command, you must authenticate with a user account or an API key
that has the Read Write role.

## Syntax

    
    
    atlas organizations apiKeys accessLists delete <entry> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
entry

|

string

|

true

|

IP or CIDR address that you want to remove from the access list. If the entry
includes a subnet mask, such as 192.0.2.0/24, use the URL-encoded value %2F
for the forward slash /.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--apiKey

|

string

|

false

|

Unique 24-digit string that identifies your API key.  
  
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
  
\--orgId

|

string

|

false

|

Organization ID to use. Overrides the settings in the configuration file or
environment variable.  
  
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

    
    
    Access list entry '<Name>' deleted  
      
  
## Examples

    
    
    # Remove the IP address 192.0.2.0 from the access list for the API key with the ID 5f24084d8dbffa3ad3f21234 in the organization with the ID 5a1b39eec902201990f12345:  
      
    atlas organizations apiKeys accessLists delete 192.0.2.0 --apiKey 5f24084d8dbffa3ad3f21234 --orgId 5a1b39eec902201990f12345  
  
What is MongoDB Atlas? →

