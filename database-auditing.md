Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up Database Auditing

Share Feedback

On this page

  * Procedure
  * Configure a Custom Auditing Filter
  * Example Auditing Filters

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

## Note

### Required Privileges

To configure audit logs, you must have the `Organization Owner` role or the
`Project Owner` role for the project that you want to update.

Database auditing lets administrators track system activity for deployments
with multiple users. Atlas administrators can select the actions, database
users, Atlas roles, and LDAP groups that they want to audit. Atlas supports
auditing most of the documented system event actions, with the following
limitations:

  * When an Atlas user performs an action in the Atlas UI on a cluster, both the audit logs and `mongodb.log` file log the `mms-automation` database user as the user performing the auditable auction. However, the Project Activity Feed logs the actual username of the Atlas user responsible for the action.

  * The Atlas audit logs don't track user creation or modification events because Atlas performs these operations directly in the `admin` database.

## Important

### Performing a Full Database Audit

Due to these noted limitations, you must use a combination of audit logs, the
`mongodb.log`, and the Project Activity Feed to perform a full audit.

The `authCheck` event action logs authorization attempts by users trying to
read from and write to databases in the clusters in your project. Atlas audits
the following specific commands:

`authCheck Reads`

|

`authCheck Writes`  
  
|  
  
aggregate

|

aggregate  
  
mapReduce

|

mapReduce  
  
distinct

|

delete  
  
eval [1]

|

eval [1]  
  
count

|

findAndModify  
  
geoNear

|

insert  
  
geoSearch

|

update  
  
group

|

resetError  
  
find

|  
  
getLastError

|  
  
getMore

|  
  
getPrevError

|  
  
parallelCollectionScan [1]

|  
  
[1]|  _(1, 2, 3)_ MongoDB versions 4.2 and later don't support these commands.  
|  
  
Atlas implements the `authCheck` event action as the following four separate
actions:

Event Action

|

Description  
  
|  
  
`authChecksReadFailures`

|

`authCheck` event action for all failed reads with the
auditAuthorizationSuccess parameter set to false. This event action is the
default for read-related event actions.  
  
`authChecksReadAll`

|

`authCheck` event action for all reads, both sucesses and failures. This event
action is the same as `authChecksReadFailures`, but with the
auditAuthorizationSuccess parameter set to true.

## Warning

If you enable auditAuthorizationSuccess, you might severely impact cluster
performance. Enable this option with caution.  
  
`authChecksWriteFailures`

|

`authCheck` event action for all failed writes with the
auditAuthorizationSuccess parameter set to false. This event action is the
default for write-related event actions.  
  
`authChecksWriteAll`

|

`authCheck` event action for all writes, both successes and failures. This
event action is the same as `authChecksWriteFailures`, but with the
auditAuthorizationSuccess parameter set to true.

## Warning

If you enable auditAuthorizationSuccess, you might severely impact cluster
performance. Enable this option with caution.  
  
To learn about how MongoDB writes audit events to disk, see Audit Guarantee in
the MongoDB Manual.

## Procedure

## Note

To learn about best practices for auditing the actions of temporary database
users, see Audit Temporary Database Users.

Use the following procedure to set up database auditing:

1

### Log in to your Atlas project.

2

### In the Security section of the left navigation, click Advanced.

3

### Toggle the button next to Database Auditing to On.

4

### Confirm that you want to audit authentication failures.

By default, Atlas logs the failed authentication attempts of both known and
unknown users in the audit log of the primary node.

5

### Select the database users, Atlas roles, and LDAP groups whose actions you
want to audit in Select users and roles.

Alternatively, click Use Custom JSON Filter to manually enter an audit filter
as a JSON string. For more information on configuring custom audit filters in
Atlas, see Configure a Custom Auditing Filter.

6

### Select the event actions that you want to audit in Select actions to
audit.

## Note

Deselecting the `authenticate` action prevents Atlas from auditing
authentication failures.

## Note

When selecting the authorization success granularity of auditing for the
`authCheck` event action, Atlas does not support different selections for
reads and writes. For example, you may not select Successes and Failures for
authCheck Reads and Failures for authCheck Writes. If you select both
authCheck Reads and authCheck Writes, Atlas automatically applies your
selected granularity to both.

7

### Click Save.

To retrieve the audit logs in Atlas, see MongoDB Logs. To retrieve the audit
logs using the API, see Logs.

## Configure a Custom Auditing Filter

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

Atlas supports specifying a JSON-formatted audit filter for customizing
MongoDB Auditing.

Custom audit filters lets users forgo the managed Atlas UI auditing filter
builder in favor of hand-tailored granular control of event auditing. Atlas
checks only that the custom filter uses valid JSON syntax, and doesn't
validate or test the filter's functionality.

The audit filter document must resolve to a query that matches one or more
fields in the audit event message. The filter document can use combinations of
query operators and equality conditions to match the desired audit messages.

To view example auditing filters, see Example Auditing Filters. To learn more
about configuring MongoDB auditing filters, see Configure Audit Filter.

## Important

Atlas uses a rolling upgrade strategy for enabling or updating audit
configuration settings across all clusters in the Atlas project. Rolling
upgrades require at least one election per replica set.

To learn more about testing application resilience to replica set elections,
see Test Primary Failover. To learn more about how Atlas provides high
availability, see Atlas High Availability.

### Procedure

1

#### Log in to your Atlas project.

2

#### In the Security section of the left navigation, click Advanced.

3

#### Toggle the button next to Database Auditing to On.

4

#### Select Use Custom JSON Filter.

5

#### Enter your audit filter into the text box.

6

#### Optional: Toggle Audit authorization successes.

## Warning

Enabling Audit authorization successes can severely impact cluster
performance. Enable this option with caution.

For audit filters specifying the `authCheck` action type, by default the
auditing system logs only authorization failures for any specified
`param.command`. Enabling Audit authorization successes directs the auditing
system to also log authorization successes. For more information, see
auditAuthorizationSuccess

7

#### Click Save.

### Edit a Custom Auditing Filter

You can edit your filter at any time:

  1. In the Security section of the left navigation, click Advanced.

  2. Under Database Auditing __ Configure Your Auditing Filter, click Use Custom JSON Filter.

  3. Make the required changes.

  4. Click Save.

## Example Auditing Filters

Use the following example auditing filters for guidance in constructing your
own filters.

## Important

These examples are not intended for use in production environments, nor are
they a replacement for familiarity with the MongoDB Auditing Documentation.

### Audit all authentication events for known users

    
    
    {  
      
      "atype": "authenticate"  
    }  
  
### Audit all authentication events for known users and authentication
failures for unknown users

    
    
    {  
      
      "$or": [  
        {  
          "users": []  
        },  
        {  
          "atype": "authenticate"  
        }  
      ]  
    }  
  
## Note

The `authenticate` action is required to log authentication failures from
known and unknown users.

### Audit authentication events for the "myClusterAdministrator" user

    
    
    {  
      
      "atype": "authenticate",  
      "param": {  
        "user": "myClusterAdministrator",  
        "db": "admin",  
        "mechanism": "SCRAM-SHA-256"  
      }  
    }  
  
### Audit unauthorized attempts at executing the selected commands

    
    
    {  
      
      "atype": "authCheck",  
      "param.command": {  
        "$in": [  
          "insert",  
          "update",  
          "delete"  
        ]  
      }  
    }  
  
← Manage Customer Keys with Google Cloud KMSView Database Access History →

