Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas dbusers describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the details for the specified database user for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas dbusers describe <username> [options]  
      
  
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

Username to retrieve from the MongoDB database. The format of the username
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
  
-h, --help

|

|

false

|

help for describe  
  
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

    
    
    # Return the details for the SCRAM SHA-authenticating database user named myDbUser:  
      
    atlas dbuser describe myDbUser --authDB admin --output json  
      
    
    # Return the details for the AWS IAM-authenticating database user with the ARN arn:aws:iam::772401394250:user/my-test-user. Prepend $external with \ to escape the special-use character:  
      
    atlas dbuser describe arn:aws:iam::772401394250:user/my-test-user --authDB \$external --output json  
      
    
    # Return the details for the X.509-authenticating database user with the RFC 2253 Distinguished Name CN=ellen@example.com,OU=users,DC=example,DC=com. Prepend $external with \ to escape the special-use character:  
      
    atlas dbuser describe CN=ellen@example.com,OU=users,DC=example,DC=com --authDB \$external --output json  
  
What is MongoDB Atlas? →

