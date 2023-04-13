Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Logs

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example
  * Example Request
  * Example Response

Retrieves a compressed (`.gz`) log file that contains a range of log messages
for a particular host in an Atlas cluster.

Process and audit logs are updated from the cluster backend infrastructure
every five minutes and contain log data from the previous five minutes. If you
are polling the API for log files, polling every five minutes is recommended.

## Example

If the logs are updated at 4:00 UTC and then you poll the API, the API returns
log data from the interval between 3:55 UTC and 4:00 UTC.

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Important

You must have the `Project Data Access Read Only` role or higher in the
project that the cluster belongs to in order to retrieve the log.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/clusters/{HOSTNAME}/logs/{LOG-NAME}  
      
  
### Request Path Parameters

Parameter

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required

|

Project identifier.  
  
`HOSTNAME`

|

Required

|

The name of the host where the log files that you want to download are stored.
To see the hostnames of your Atlas cluster, use the
/api/atlas/v1.0/groups/{GROUP-ID}/clusters endpoint.  
  
`LOG-NAME`

|

Required

|

The name of the log file that you want to retrieve:

  * mongodb.gz

  * mongos.gz

  * `mongodb-audit-log.gz`

  * `mongos-audit-log.gz`

## Note

Audit logs are only available if you have enabled Database Auditing for an
Atlas project.

  
  
### Request Query Parameters

Field

|

Required/Optional

|

Description  
  
||  
  
`startDate`

|

Optional.

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch that
specifies starting point for the range of log messages to retrieve. Default is
24 hours prior to the current timestamp.  
  
`endDate`

|

Optional.

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch that
specifies the end point for the range of log messages to retrieve. Default is
current timestamp.  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response Elements

The endpoint responds with a compressed log file `mongodb.gz`.

## Example

This example downloads the log file to the directory from which you made the
request.

### Example Request

The following example downloads the server log for the `mongod` instance
running on the specified host:

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
     --header 'Accept: application/gzip' \  
     --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{HOSTNAME}/logs/mongodb.gz" \  
     --output "mongodb.gz"  
  
### Example Response

The `curl` command in this example saves the log file to `mongodb.gz` and
shows the following progress output.

    
    
    %     Total  % Received % Xferd  Average  Speed   Time    Time     Time  Current  
      
                                     Dload    Upload  Total   Spent    Left  Speed  
    100   106     100       106      0        0       134     0 --:--:-- -   134  
  
What is MongoDB Atlas? →

