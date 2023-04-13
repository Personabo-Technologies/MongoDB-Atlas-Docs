Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Verify Connect via Peering Only Mode for a Project

Share Feedback

On this page

  * Resource
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

### Deprecated Feature

This feature has been deprecated. Use Split Horizon connection strings to
connect to your cluster. These connection strings allow you to connect using
both VPC/VNet Peering and allowed public IP addresses. To learn more about
support for Split Horizon, see this FAQ. Use the Disable Connect via Peering
Only Mode for a Project endpoint to disable Peering Only.

Verify whether an Atlas project has enabled Connect via Peering Only mode. You
must have the `Project Read Only` role to successfully call this endpoint.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/privateIpMode  
      
  
### Request Path Parameters

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`GROUP-ID`

|

string

|

Required

|

Unique identifier of N Atlas project for which you want to enable Connect via
Peering Only mode.  
  
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

This endpoint doesn't use HTTP request body parameters.

## Response

Response Element

|

Type

|

Description  
  
||  
  
enabled

|

boolean

|

Indicates whether Connect via Peering Only mode is enabled or disabled for an
Atlas project.  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --include \  
    4|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateIpMode?pretty=true"  
  
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

    
    
    1| {  
    |  
    2|   "enabled" : true  
    3| }  
  
What is MongoDB Atlas? →

