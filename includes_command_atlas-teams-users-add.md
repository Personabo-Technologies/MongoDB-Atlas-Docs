Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas teams users add

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Add the specified MongoDB user to a team for your organization.

Users must be current members of your organization before you can add them to
a team.

To use this command, you must authenticate with a user account or an API key
that has the Organization User Admin role.

## Syntax

    
    
    atlas teams users add <userId>... [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
userId

|

string

|

true

|

Unique 24-digit string that identifies the user. You can add more than one
user at a time by specifying multiple user IDs separated by a space.  
  
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

help for add  
  
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
  
\--teamId

|

string

|

true

|

Unique 24-digit string that identifies the team.  
  
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

    
    
    # Add the users with the IDs 5dd58c647a3e5a6c5bce46c7 and 5dd56c847a3e5a1f363d424d to the team with the ID 5f6a5c6c713184005d72fe6e for the organization with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas teams users add 5dd58c647a3e5a6c5bce46c7 5dd56c847a3e5a1f363d424d --teamId 5f6a5c6c713184005d72fe6e --orgId 5e1234c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

