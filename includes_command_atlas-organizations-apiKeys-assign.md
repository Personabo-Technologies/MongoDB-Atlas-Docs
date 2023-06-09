Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations apiKeys assign

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Modify the roles or description for the specified organization API key.

When you modify the roles for an organization API key with this command, the
values you specify overwrite the existing roles assigned to the API key.

To view possible values for the apiKeyId argument, run atlas organizations
apiKeys list.

To use this command, you must authenticate with a user account or an API key
that has the Organization User Admin role.

## Syntax

    
    
    atlas organizations apiKeys assign <apiKeyId> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
apiKeyId

|

string

|

true

|

Unique 24-digit string that identifies your API key.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--desc

|

string

|

false

|

Description of the API key.  
  
-h, --help

|

|

false

|

help for assign  
  
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

false

|

Role or roles that you want to assign to the API key. To assign more than one
role, you can specify each role with a separate role flag or specify all of
the roles as a comma-separated list using one role flag. Valid values are
ORG_OWNER, ORG_MEMBER, ORG_GROUP_CREATOR, ORG_BILLING_ADMIN, and
ORG_READ_ONLY.  
  
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

    
    
    API Key '<ID>' successfully updated.  
      
  
## Examples

    
    
    # Modify the role and description for the API key with the ID 5f24084d8dbffa3ad3f21234 for the organization with the ID 5a1b39eec902201990f12345:  
      
    atlas organizations apiKeys assign 5f24084d8dbffa3ad3f21234 --role ORG_MEMBER --desc "User1 Member Key" --orgId 5a1b39eec902201990f12345 --output json  
  
What is MongoDB Atlas? →

