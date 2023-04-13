Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas projects apiKeys create

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create an organization API key and assign it to your project.

MongoDB returns the private API key only once. After you run this command,
immediately copy, save, and secure both the public and private API keys.

To use this command, you must authenticate with a user account or an API key
that has the Project User Admin role.

## Syntax

    
    
    atlas projects apiKeys create [options]  
      
  
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
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
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

    
    
    # Create an organization API key with the ORG_OWNER role and assign it to the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas projects apiKeys create --desc "My API key" --projectId 5e1234c17a3e5a48f5497de3 --role ORG_OWNER --output json  
  
What is MongoDB Atlas? →

