Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations invitations invite

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Invite the specified MongoDB user to your organization.

To use this command, you must authenticate with a user account or an API key
that has the Organization User Admin role.

## Syntax

    
    
    atlas organizations invitations invite <email> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
email

|

string

|

true

|

Email address that belongs to the user that you want to invite to the
organization.  
  
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

help for invite  
  
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
  
\--role

|

strings

|

true

|

User's roles for the associated organization. Valid values include ORG_OWNER,
ORG_MEMBER, ORG_GROUP_CREATOR, ORG_BILLING_ADMIN, and ORG_READ_ONLY.  
  
\--teamId

|

strings

|

false

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

    
    
    # Invite the MongoDB user with the email user@example.com to the organization with the ID 5f71e5255afec75a3d0f96dc with ORG_OWNER access:  
      
    atlas organizations invitations invite user@example.com --orgId 5f71e5255afec75a3d0f96dc --role ORG_OWNER --output json  
  
What is MongoDB Atlas? →

