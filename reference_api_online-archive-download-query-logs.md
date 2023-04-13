Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Download Online Archive Query Logs

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Response Elements
  * Example
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

You can download the online archive query logs using the API or the Atlas UI.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Required Roles

You must have `Project Data Access Read Only` or higher role to download the
query logs for online archives.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/queryLogs.gz  
      
  
## Request Parameters

### Request Path Parameters

Path Element

|

Necessity

|

Description  
  
||  
  
`GROUP-ID`

|

Required

|

Unique identifier of the project that contains the specified cluster.  
  
`CLUSTER-NAME`

|

Required

|

Name of the cluster.  
  
### Request Query Parameters

Field

|

Necessity

|

Description  
  
||  
  
`archiveOnly`

|

Optional

|

Flag that indicates whether to download logs for queries against your online
archive only or both your online archive and cluster. Value can be one of the
following:

  * `true` \- to download logs for queries on online archive only

  * `false` \- to download logs for queries on both cluster and online archive

If omitted, defaults to `false`.  
  
`endDate`

|

Optional

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch that
specifies the end point for the range of log messages to retrieve. Default is
the current timestamp.  
  
`startDate`

|

Optional

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch that
specifies starting point for the range of log messages to retrieve. Default is
4 hours prior to the current timestamp.  
  
## Response Elements

The endpoint downloads to your current working directory a compressed log file
with either the name you specified using the `--output` option or the default
filename if you specified the `-OJ` option. The default filename varies based
on whether you are downloading logs for queries against your online archive
only or both your online archive and cluster.

Online Archive Only

Online Archive and Cluster

    
    
    <cluster-name>_archive_only_<startdate>_<enddate>_queries.log.gz  
      
  
## Example

The following example command downloads the logs for queries against the
online archive only to a file named `oaquerylog.gz`. It downloads the log file
to the directory from which you made the request.

### Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/gzip" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/queryLogs.gz?archiveOnly=true" \  
         --output "oaquerylog.gz"  
  
### Example Response

The `curl` command in this example saves the log file to `oaquerylog.gz` in
the current working directory and shows the following progress output.

    
    
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current  
      
                                  Dload  Upload   Total   Spent    Left  Speed  
    100   106  100   106    0     0    233      0 --:--:-- --:--:-- --:--:--   233  
    100 2683k    0 2683k    0     0   541k      0 --:--:--  0:00:04 --:--:--  755k  
  
What is MongoDB Atlas? →

