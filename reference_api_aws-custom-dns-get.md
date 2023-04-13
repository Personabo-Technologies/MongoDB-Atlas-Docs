Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Custom DNS Configuration for Atlas Clusters on AWS

Share Feedback

On this page

  * Required Roles
  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Retrieve the custom DNS configuration of an Atlas project's clusters deployed
to AWS.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You can successfully call this endpoint with any assigned role.

## Request

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/awsCustomDNS  
      
  
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

Unique identifier for the project.  
  
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

## Response

Field

|

Type

|

Description  
  
||  
  
`enabled`

|

boolean

|

Indicates whether the project's clusters deployed to AWS use custom DNS.

If `true`, the Get All Clusters and Get One Cluster endpoints return the
`connectionStrings.private` and `connectionStrings.privateSrv` fields for
clusters deployed to AWS.  
  
## Example Request

    
    
    curl -X GET -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/awsCustomDNS"  
      
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    {  
      
        "enabled": true  
    }  
  
What is MongoDB Atlas? →

