Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas teams create

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Create a team for your organization.

To use this command, you must authenticate with a user account or an API key
that has the Organization Owner role.

## Syntax

    
    
    atlas teams create <name> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
name

|

string

|

true

|

Label that identifies the team.  
  
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
  
\--username

|

strings

|

true

|

Comma-separated list of valid usernames for the MongoDB users you want to add
to the new team. A team must have at least one user. New users must accept the
invitation to join an organization before you can add them to a team.  
  
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

    
    
    Team '<Name>' created.  
      
  
## Examples

    
    
    # Create a team named myTeam in the organization with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas teams create myTeam --username user1@example.com,user2@example.com --orgId 5e1234c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

