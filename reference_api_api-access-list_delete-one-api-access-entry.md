Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete One Access List Entry for One Organization API Key

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

Delete a specified restricted IP address or CIDR block from the specified API
Key.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    DELETE /orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/{IP-ADDRESS}  
      
  
### Request Path Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
ORG-ID

|

string

|

Required

|

Unique identifier for the organization to which the target API key belongs.
Use the /orgs endpoint to retrieve all organizations to which the
authenticated user has access.  
  
API-KEY-ID

|

string

|

Required

|

Unique identifier for the API key for which you want to retrieve access list
entries. Use the /orgs/{ORG-ID}/apiKeys endpoint to retrieve all API keys for
the specified organization to which the authenticated user has access.  
  
ACCESS-LIST-ENTRY

|

string

|

Required

|

IP address or CIDR block. If the entry includes a subnet mask, such as
`192.0.2.0/24`, use the URL-encoded value `%2F` for the forward slash `/`.  
  
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

This endpoint returns an empty JSON object.

## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/192.0.2.0%2F24"  
  
## Example Response

### Response Header

    
    
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
  
### Response Body

This endpoint returns an empty JSON object.

What is MongoDB Atlas? →

