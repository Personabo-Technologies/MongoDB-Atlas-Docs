Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations invitations describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the specified pending invitation to your organization.

To use this command, you must authenticate with a user account or an API key
that has the Organization User Admin role.

## Syntax

    
    
    atlas organizations invitations describe <invitationId> [options]  
      
  
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

true

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
  
-h, --help

|

|

false

|

help for describe  
  
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

    
    
    # Return the JSON-formatted details of the pending invitation with the ID 5dd56c847a3e5a1f363d424d for the organization with the ID 5f71e5255afec75a3d0f96dc:  
      
    atlas organizations invitations describe 5dd56c847a3e5a1f363d424d --orgId 5f71e5255afec75a3d0f96dc --output json  
  
What is MongoDB Atlas? →

