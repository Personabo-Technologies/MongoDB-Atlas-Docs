Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas events projects list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Return all events for the specified project.

## Syntax

    
    
    atlas events projects list [options]  
      
  
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

help for list  
  
\--limit

|

int

|

false

|

Number of items per results page.  
  
\--maxDate

|

string

|

false

|

Returns events whose created date is less than or equal to it.  
  
\--minDate

|

string

|

false

|

Returns events whose created date is greater than or equal to it.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--page

|

int

|

false

|

Page number that specifies a page of results.  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
\--type

|

strings

|

false

|

Type of event that triggered the alert. Valid values are
AWS_ENCRYPTION_KEY_NEEDS_ROTATION, AZURE_ENCRYPTION_KEY_NEEDS_ROTATION,
CLUSTER_MONGOS_IS_MISSING, CPS_RESTORE_FAILED, CPS_RESTORE_SUCCESSFUL,
CPS_SNAPSHOT_BEHIND, CPS_SNAPSHOT_DOWNLOAD_REQUEST_FAILED,
CPS_SNAPSHOT_FALLBACK_FAILED, CPS_SNAPSHOT_FALLBACK_SUCCESSFUL,
CPS_SNAPSHOT_SUCCESSFUL, CREDIT_CARD_ABOUT_TO_EXPIRE,
DAILY_BILL_OVER_THRESHOLD, GCP_ENCRYPTION_KEY_NEEDS_ROTATION, HOST_DOWN,
JOINED_GROUP, NDS_X509_USER_AUTHENTICATION_CUSTOMER_CA_EXPIRATION_CHECK,
NDS_X509_USER_AUTHENTICATION_MANAGED_USER_CERTS_EXPIRATION_CHECK, NO_PRIMARY,
OUTSIDE_METRIC_THRESHOLD, OUTSIDE_SERVERLESS_METRIC_THRESHOLD,
OUTSIDE_REALM_METRIC_THRESHOLD, PENDING_INVOICE_OVER_THRESHOLD,
PRIMARY_ELECTED, REMOVED_FROM_GROUP, REPLICATION_OPLOG_WINDOW_RUNNING_OUT,
TOO_MANY_ELECTIONS, USER_ROLES_CHANGED_AUDIT, USERS_WITHOUT_MULTIFACTOR_AUTH.  
  
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

    
    
    # Return a JSON-formatted list of events for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas events projects list --Id 5e2211c17a3e5a48f5497de3 --output json  
  
What is MongoDB Atlas? →

