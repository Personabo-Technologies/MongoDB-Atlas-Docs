Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# View Database Access History

Share Feedback

On this page

  * Overview
  * Procedure

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

## Note

To view database access history, you must have either the `Project Owner` or
`Organization Owner` role.

## Overview

Atlas parses the MongoDB database logs to collect a list of authentication
requests made against your clusters through the following methods:

  * `mongosh`

  * Compass

  * Drivers

Authentication requests made with API Keys through the Atlas Administration
API are not logged.

Atlas logs the following information for each authentication request within
the last 7 days:

Field

|

Description  
  
|  
  
Timestamp

|

The date and time of the authentication request.  
  
Username

|

The username associated with the database user who made the authentication
request.

For LDAP usernames, the UI displays the resolved LDAP name. Hover over the
name to see the full LDAP username.  
  
IP Address

|

The IP address of the machine that sent the authentication request.  
  
Host

|

The target server that processed the authentication request.  
  
Authentication Source

|

The database that the authentication request was made against. `admin` is the
authentication source for SCRAM-SHA users and `$external` for LDAP users.  
  
Authentication Result

|

The success or failure of the authentication request. A reason code is
displayed for the failed authentication requests.  
  
Authentication requests are pre-sorted by descending timestamp with 25 entries
per page.

### Logging Limitations

If a cluster experiences an activity spike and generates an extremely large
quantity of log messages, Atlas may stop collecting and storing new logs for a
period of time.

## Note

Log analysis rate limits apply only to the Performance Advisor UI, the Query
Profiler UI, and the Access Tracking UI. Downloadable log files are always
complete.

If authentication requests occur during a period when logs are not collected,
they will not appear in the database access history.

## Procedure

Atlas CLI

Atlas Administration API

Atlas UI

To return the access logs for a cluster using the Atlas CLI, run the following
command:

    
    
    atlas accessLogs list [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas accessLogs list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Set Up Database AuditingConfigure Access to the Atlas UI →

