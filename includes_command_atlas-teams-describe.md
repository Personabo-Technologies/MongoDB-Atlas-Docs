Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas teams describe

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return the details for the specified team for your organization.

You can return the details for a team using the team's ID or the team's name.
You must specify either the id option or the name option.

To use this command, you must authenticate with a user account or an API key
that has the Organization Member role.

## Syntax

    
    
    atlas teams describe [options]  
      
  
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

help for describe  
  
\--id

|

string

|

false

|

Unique 24-digit string that identifies the team.  
  
\--name

|

string

|

false

|

Label that identifies the team.  
  
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
  
## Examples

    
    
    # Return the JSON-formatted details for the the team with the ID 5e44445ef10fab20b49c0f31 in the organization with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas teams describe --id 5e44445ef10fab20b49c0f31 --projectId 5e1234c17a3e5a48f5497de3 --output json  
      
    
    # Return the JSON-formatted details for the the team with the name myTeam in the organization with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas teams describe --name myTeam --projectId 5e1234c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

