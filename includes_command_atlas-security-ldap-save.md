Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas security ldap save

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Save an LDAP configuration for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas security ldap save [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--authenticationEnabled

|

|

false

|

Specifies whether user authentication with LDAP is enabled.  
  
\--authorizationEnabled

|

|

false

|

Specifies whether user authorization with LDAP is enabled.  
  
\--authzQueryTemplate

|

string

|

false

|

RFC 4515- and RFC 4516-formatted LDAP query template that Atlas executes to
obtain the LDAP authorization groups to which the authenticated user belongs.
Use the {USER} placeholder in the URL to substitute the username. The query is
relative to the host specified with the hostname.  
  
\--bindPassword

|

string

|

false

|

Password used to authenticate the bindUsername.  
  
\--bindUsername

|

string

|

true

|

User distinguished name (DN) that Atlas uses to connect to the LDAP server.
LDAP distinguished names must be formatted according to RFC 2253.  
  
\--caCertificate

|

string

|

false

|

Certificate Authority (CA) used to verify the identity of the LDAP server. To
delete an assigned value, pass an empty string.  
  
-h, --help

|

|

false

|

help for save  
  
\--hostname

|

string

|

true

|

Hostname or IP address of the LDAP server.  
  
\--mappingLdapQuery

|

string

|

false

|

RFC 4515- and RFC 4516-formatted LDAP query template that inserts the LDAP
name that the regex matches into an LDAP query URI.  
  
\--mappingMatch

|

string

|

false

|

ECMAScript-formatted regular expression (regex) to match against a provided
username.  
  
\--mappingSubstitution

|

string

|

false

|

LDAP distinguished name (DN) template that converts the LDAP username that
matches the regex specified in match into an LDAP DN.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--port

|

int

|

false

|

Port to which the LDAP server listens to for client connections. This value
defaults to 636.  
  
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

    
    
    # Save an LDAP server configuration to authenticate and authorize MongoDB users for the host atlas-ldaps-01.ldap.myteam.com:  
      
    atlas security ldap save --authenticationEnabled --authorizationEnabled  
    --hostname atlas-ldaps-01.ldap.myteam.com --bindUsername  
    "CN=Administrator,CN=Users,DC=atlas-ldaps-01,DC=myteam,DC=com"  
    --bindPassword changeMe  
  
What is MongoDB Atlas? →

