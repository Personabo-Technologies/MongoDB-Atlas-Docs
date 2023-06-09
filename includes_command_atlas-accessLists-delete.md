Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas accessLists delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified IP access list entry from your project.

The command prompts you to confirm the operation when you run the command
without the force option.

To use this command, you must authenticate with a user account or an API key
that has the Read Write role.

## Syntax

    
    
    atlas accessLists delete <entry> [options]  
      
  
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

The IP address, CIDR address, or AWS security group ID that you want to remove
from the access list.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
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

    
    
    Project access list entry '<Name>' deleted  
      
  
## Examples

    
    
    # Remove the IP address 192.0.2.0 from the access list for the project with the ID 5e2211c17a3e5a48f5497de3 after prompting for a confirmation:  
      
    atlas accessLists delete 192.0.2.0 --projectId 5e2211c17a3e5a48f5497de3  
      
    
    # Remove the IP address 192.0.2.0 from the access list for the project with the ID 5e2211c17a3e5a48f5497de3 without requiring confirmation:  
      
    atlas accessLists delete 192.0.2.0 --projectId 5e2211c17a3e5a48f5497de3 --force  
  
What is MongoDB Atlas? →

