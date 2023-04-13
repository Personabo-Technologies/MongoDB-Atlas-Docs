Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations create

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Create an Ops Manager or Cloud Manager organization. This command is
unavailable for Atlas.

## Syntax

    
    
    atlas organizations create <name> [options]  
      
  
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

Label that identifies the organization.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--apiKeyDescription

|

string

|

false

|

Description of the API key.  
  
\--apiKeyRole

|

strings

|

false

|

Role or roles that you want to assign to the API key. To assign more than one
role, you can specify each role with a separate role flag or specify all of
the roles as a comma-separated list using one role flag. Valid values are
ORG_OWNER, ORG_MEMBER, ORG_GROUP_CREATOR, ORG_BILLING_ADMIN, and
ORG_READ_ONLY.  
  
-h, --help

|

|

false

|

help for create  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--ownerId

|

string

|

false

|

Unique 24-digit string that identifies the Atlas user to be granted the Org
Owner role on the specified organization. Required if using API keys.  
  
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

    
    
    # Create an Atlas organization with the name myOrg:  
      
    atlas organizations create myOrg --output json  
  
What is MongoDB Atlas? →

