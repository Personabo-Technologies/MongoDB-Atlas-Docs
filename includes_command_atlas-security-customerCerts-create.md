Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas security customerCerts create

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Saves a customer-managed X.509 configuration for your project.

Saving a customer-managed X.509 configuration triggers a rolling restart.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas security customerCerts create [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--casFile

|

string

|

true

|

Path to a PEM file containing one or more CAs for database user
authentication.  
  
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

    
    
    Certificate successfully created.  
      
  
## Examples

    
    
    # Save the file named ca.pem stored in the files directory to the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas security customerCerts create --casFile files/ca.pem --projectId 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

