Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations invitations update

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Modifies the details of the specified pending invitation to your organization.

You can use either the invitation ID or the user's email address to specify
the invitation.

To use this command, you must authenticate with a user account or an API key
that has the Organization Owner role.

## Syntax

    
    
    atlas organizations invitations update [invitationId] [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
invitationId

|

string

|

false

|

Unique 24-digit string that identifies the invitation.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--email

|

string

|

false

|

Email address for the user.  
  
-h, --help

|

|

false

|

help for update  
  
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

    
    
    Invitation <ID> updated.  
      
  
## Examples

    
    
    # Modify the pending invitation with the ID 5dd56c847a3e5a1f363d424d to grant ORG_OWNER access the organization with the ID 5f71e5255afec75a3d0f96dc:  
      
    atlas organizations invitations update 5dd56c847a3e5a1f363d424d --orgId 5f71e5255afec75a3d0f96dc --role ORG_OWNER --output json  
      
    
    # Modify the invitation for the user with the email address user@example.com to grant ORG_OWNER access the organization with the ID 5f71e5255afec75a3d0f96dc:  
      
    atlas organizations invitations update --email user@example.com --orgId 5f71e5255afec75a3d0f96dc --role ORG_OWNER --output json  
  
What is MongoDB Atlas? →

