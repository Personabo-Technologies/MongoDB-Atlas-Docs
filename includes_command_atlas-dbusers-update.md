Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas dbusers update

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Modify the details for a database user for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas dbusers update <username> [options]  
      
  
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

Username to update in the MongoDB database.  
  
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

help for update  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
-p, --password

|

string

|

false

|

Password for the user.  
  
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

false

|

User's roles and the databases or collections on which the roles apply.  
  
\--scope

|

strings

|

false

|

Array of clusters and Atlas Data Lakes that this user has access to.  
  
-u, --username

|

string

|

false

|

Username for authenticating to MongoDB.  
  
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

    
    
    Successfully updated database user '<Username>'.  
      
  
## Examples

    
    
    # Update roles for a database user named myUser for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas dbuser update myUser --role readWriteAnyDatabase --projectId 5e2211c17a3e5a48f5497de3  
      
    
    # Update scopes for a database user named myUser for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas dbuser update myUser --scope resourceName:resourceType --projectId 5e2211c17a3e5a48f5497de3  
  
What is MongoDB Atlas? →

