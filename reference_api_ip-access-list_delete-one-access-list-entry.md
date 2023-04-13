Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete an Entry from the Project IP Access List

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response
  * Example Header
  * Example Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Access List Replaces Whitelist

This resource replaces the whitelist resource. Atlas removed whitelists in
July 2021. Update your applications to use this new resource.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Important

The `/groups/{GROUP-ID}/accessList` endpoint manages the database IP access
list. This endpoint is distinct from the orgs/{ORG-ID}/apiKeys/{API-KEY-
ID}/accesslist endpoint, which manages the access list for Atlas
organizations.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Syntax

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    DELETE /groups/{GROUP-ID}/accessList/{ACCESS-LIST-ENTRY}  
      
  
### Request Path Parameters

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
GROUP-ID

|

string

|

Required

|

Unique identifier for the project for which you want to delete an access list
entry.  
  
ACCESS-LIST-ENTRY

|

string

|

Required

|

Can be either the:

  * AWS security group ID,

  * IP address, or

  * CIDR address

of the access list entry to delete. If the entry includes a subnet mask, such
as `192.0.2.0/24`, use the URL-encoded value `%2F` for the forward slash `/`.

## Important

When you remove an entry from the IP access list, existing connections from
the removed address(es) may remain open for a variable amount of time. How
much time passes before Atlas closes the connection depends on several
factors, including:

  * how the connection was established

  * how the application or driver using the address behaves

  * which protocol (like TCP or UDP) the connection uses

  
  
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

This endpoint does not have response elements.

## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/accessList/192.0.2.0%2F24" \  
  
## Example Response

### Example Header

    
    
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
  
### Example Body

This endpoint doesn't return a response body.

What is MongoDB Atlas? →

