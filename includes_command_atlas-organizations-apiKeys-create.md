Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations apiKeys create

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create an API Key for your organization.

MongoDB returns the private API key only once. After you run this command,
immediately copy, save, and secure both the public and private API keys.

To use this command, you must authenticate with a user account or an API key
that has the Organization User Admin role.

## Syntax

    
    
    atlas organizations apiKeys create [options]  
      
  
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

true

|

Description of the API key.  
  
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
  
\--role

|

strings

|

true

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

    
    
    API Key '<ID>' created.  
      
    Public API Key <PublicKey>  
    Private API Key <PrivateKey>  
  
## Examples

    
    
    # Create an organization API key with organization owner access in the organization with the ID 5a1b39eec902201990f12345:  
      
    atlas organizations apiKeys create --role ORG_OWNER --desc "My API Key" --orgId 5a1b39eec902201990f12345 --output json  
  
What is MongoDB Atlas? →

