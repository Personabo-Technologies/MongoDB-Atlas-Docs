Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Enable Managed Slow Operation Threshold

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Example Response
  * Response Headers

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Enable Atlas management of the slow operation threshold for your cluster. The
slow operation threshold determines which operations are flagged by the
Performance Advisor and Query Profiler.

  * When `enabled`, Atlas uses the average execution time for operations on your cluster to determine slow-running queries. As a result, the threshold is more pertinent to your cluster workload.

  * When `disabled`, Atlas considers any operation that takes longer than 100 milliseconds to be slow.

To learn how to disable Atlas-managed slow operation threshold, see Disable
Managed Slow Operation Threshold.

Atlas-managed slow operation threshold is enabled by default for dedicated
clusters (`M10+`).

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

To access this endpoint, you must have the `Project Owner` role.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    POST /groups/{GROUP-ID}/managedSlowMs/enable  
      
  
### Request Path Parameters

Path Element

|

Description  
  
|  
  
`GROUP-ID`

|

The unique identifier for the project where the the MongoDB host resides.  
  
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

This endpoint doesn't return a response body.

## Example Request

The following request enables the Atlas-managed slow operation threshold.

    
    
     curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest -i \  
      
    --header "Accept: application/json" \  
    --header "Content-Type: application/json" \  
    --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/6ad58c7d7a3e5b2c5bce0009/managedSlowMs/enable"  
  
## Example Response

### Response Headers

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 204 No Content  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
What is MongoDB Atlas? →

