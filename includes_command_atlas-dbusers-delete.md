Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas dbusers delete

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Remove the specified database user from your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas dbusers delete <username> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
username

|

string

|

true

|

Username to delete from the MongoDB database. The format of the username
depends on the user's method of authentication.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--authDB

|

string

|

false

|

Authentication database name. If the user authenticates with AWS IAM, x.509,
or LDAP, this value should be $external. If the user authenticates with SCRAM-
SHA, this value should be admin. This value defaults to "admin".  
  
\--force

|

|

false

|

Flag that indicates whether to skip the confirmation prompt before proceeding
with the requested action.  
  
-h, --help

|

|

false

|

help for delete  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
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

    
    
    DB user '<Name>' deleted  
      
  
## Examples

    
    
    # Delete the SCRAM SHA-authenticating database user named dylan for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas dbusers delete dylan --projectId 5e2211c17a3e5a48f5497de3  
      
    
    # Delete the AWS IAM-authenticating database user with the ARN arn:aws:iam::123456789012:user/sales/enterprise/DylanBloggs for the project with ID 5e2211c17a3e5a48f5497de3. Prepend $external with \ to escape the special-use character:  
      
    atlas dbusers delete arn:aws:iam::123456789012:user/sales/enterprise/DylanBloggs --authDB \$external --projectId 5e2211c17a3e5a48f5497de3  
      
    
    # Delete the xLDAP-authenticating database user with the RFC 2253 Distinguished Name CN=Dylan Bloggs,OU=Enterprise,OU=Sales,DC=Example,DC=COM for the project with ID 5e2211c17a3e5a48f5497de3. Prepend $external with \ to escape the special-use character:  
      
    atlas dbusers delete CN=Dylan Bloggs,OU=Enterprise,OU=Sales,DC=Example,DC=COM --authDB \$external --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

