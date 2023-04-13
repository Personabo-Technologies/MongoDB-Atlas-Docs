Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Cancel One Cloud Backup Restore Job

Share Feedback

On this page

  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Example Response

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

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    DELETE /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs/{JOB-ID}  
      
  
### Request Path Parameters

Path Element

|

Description  
  
|  
  
`GROUP-ID`

|

The unique identifier of the project for the Atlas cluster.  
  
`CLUSTER-NAME`

|

The name of the Atlas cluster whose restore job you want to cancel.  
  
`JOB-ID`

|

The unique identifier of the restore job to cancel. You can only cancel manual
download restore jobs. Use the Get One Restore Job Endpoint to confirm the
restoration job type.  
  
### Request Query Parameters

This endpoint might use any of the HTTP request query parameters available to
all Atlas Administration API resources. All of these are optional.

Name

|

Type

|

Necessity

|

Description

|

Default  
  
||||  
  
pretty

|

boolean

|

Optional

|

Flag indicating whether the response body should be in a prettyprint format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag indicating if Atlas should wrap the response in a JSON envelope.

This option may be needed for some API clients. These clients cannot access
the HTTP response headers or status code. To remediate this, set
**envelope=true** in the query.

For endpoints that return one result, the response body includes:

|

|  
  
|  
  
status

|

HTTP response code  
  
envelope

|

Expected response body  
  
`false`  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response Elements

This endpoint does not have response elements.

## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
      --header "Accept: application/json" \  
      --header "Content-Type: application/json" \  
      --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b6212af90dc76637950a2c6/clusters/MyCluster/backup/restoreJobs/5b622f7087d9d6039fafe03f"  
  
## Example Response

This endpoint doesn't return a response body.

What is MongoDB Atlas? →

