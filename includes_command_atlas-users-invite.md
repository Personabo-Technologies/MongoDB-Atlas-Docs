Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas users invite

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Create a MongoDB user for your MongoDB application and invite the MongoDB user
to your organizations and projects.

A MongoDB user account grants access only to the the MongoDB application. To
grant database access, create a database user with atlas dbusers create.

## Syntax

    
    
    atlas users invite [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--country

|

string

|

false

|

ISO 3166-1 alpha two-letter country code of the user's geographic location.
Required for the Atlas CLI.  
  
\--email

|

string

|

true

|

Email address for the user.  
  
\--firstName

|

string

|

true

|

First or given name for the user.  
  
-h, --help

|

|

false

|

help for invite  
  
\--lastName

|

string

|

true

|

Last name, family name, or surname for the user.  
  
\--mobile

|

string

|

false

|

Mobile phone number for the user.  
  
\--orgRole

|

strings

|

false

|

Unique 24-digit string that identifies the organization, colon, and the user's
role for the organization. Specify this value as orgID:ROLE. Valid values for
ROLE include ORG_OWNER, ORG_MEMBER, ORG_GROUP_CREATOR, ORG_BILLING_ADMIN, and
ORG_READ_ONLY.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--password

|

string

|

false

|

Password for the user.  
  
\--projectRole

|

strings

|

false

|

Unique 24-digit string that identifies the project, colon, and the user's role
for the project. Specify this value as projectID:ROLE. Valid values for ROLE
include GROUP_CLUSTER_MANAGER, GROUP_DATA_ACCESS_ADMIN,
GROUP_DATA_ACCESS_READ_ONLY, GROUP_DATA_ACCESS_READ_WRITE, GROUP_OWNER, and
GROUP_READ_ONLY.  
  
\--username

|

string

|

true

|

Username that identifies the user. This value must be a valid email address.  
  
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

    
    
    # Create the MongoDB user with the username user@example.com and invite them to the organization with the ID 5dd56c847a3e5a1f363d424d with ORG_OWNER access:  
      
    atlas users invite --email user@example.com --username user@example.com --orgRole 5dd56c847a3e5a1f363d424d:ORG_OWNER --firstName Example --lastName User --country US --output json  
      
    
    # Create the MongoDB user with the username user@example.com and invite them to the project with the ID 5f71e5255afec75a3d0f96dc with GROUP_READ_ONLY access:  
      
    atlas users invite --email user@example.com --username user@example.com --projectRole 5f71e5255afec75a3d0f96dc:GROUP_READ_ONLY --firstName Example --lastName User --country US --output json  
  
What is MongoDB Atlas? →

