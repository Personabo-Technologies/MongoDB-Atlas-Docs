Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas dbusers certs create

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create a new Atlas-managed X.509 certificate for the specified database user.

The user you specify must authenticate using X.509 certificates. You can't use
this command to create certificates if you are managing your own Certificate
Authority (CA) in self-managed X.509 mode.

## Syntax

    
    
    atlas dbusers certs create [options]  
      
  
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
  
\--monthsUntilExpiration

|

int

|

false

|

Number of months until the X.509 certificate expires. This value defaults to
3.  
  
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
  
\--username

|

string

|

true

|

Username of a database user.  
  
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

    
    
    <Certificate>  
      
  
## Examples

    
    
    # Create an Atlas-managed X.509 certificate that expires in 5 months for a MongoDB user named dbuser for the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas dbusers certs create --username dbuser --monthsUntilExpiration 5 --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

