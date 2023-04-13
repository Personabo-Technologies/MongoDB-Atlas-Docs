Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Download Query Logs for One Federated Database Instance

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

Use this endpoint to download query logs for a specific federated database
instance.

## Required Roles

You must have `Project Data Access Read Only` or higher role to download the
query logs for your federated database instance.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/dataFederation/{NAME}/queryLogs.gz  
      
  
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

Unique identifier for the project that contains the federated database
instance for which you want to download query logs.  
  
`NAME`

|

Required

|

Name of the federated database instance for which you want to download query
logs.

You can use the Get All Federated Database Instances endpoint to retrieve all
federated database instances associated with the project. The `name` field in
the response of that endpoint corresponds to the `NAME` parameter here.  
  
### Request Query Parameters

Field

|

Necessity

|

Description  
  
||  
  
`endDate`

|

Optional

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch that
specifies the end point for the range of log messages to retrieve. Default is
current timestamp.  
  
`startDate`

|

Optional

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch that
specifies starting point for the range of log messages to retrieve. Default is
4 hours before the current timestamp.  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

The endpoint downloads a compressed log file to your current working directory
with either the name you specified using the `--output` option or the default
filename in the following format if you specified the `-OJ` option:

    
    
    <data-lake-name>_<startdate>_<enddate>_queries.log.gz  
      
  
## Example

The following example command downloads the logs for queries on the federated
database instance to a file named `dataLakeQueryLog.gz`. The command downloads
the log file to the directory from which you made the request.

### Request

    
    
    curl -u "username:apiKey" --digest \  
      
     --header "Accept: application/gzip" \  
     --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/dataFederation/{NAME}/queryLogs.gz" \  
     --output "dataFederationQueryLog.gz"  
  
### Response

The example `curl` command saves the log file to `dataFederationQueryLog.gz`
in the current working directory and shows the following progress output.

    
    
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current  
      
                                   Dload  Upload   Total   Spent    Left  Speed  
    100   106  100   106    0     0    301      0 --:--:-- --:--:-- --:--:--   301  
    100 62883    0 62883    0     0  65915      0 --:--:-- --:--:-- --:--:--  374k  
  
What is MongoDB Atlas? →

