Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete an Atlas Search Index

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `fts` resource allows you to retrieve and edit Atlas Search analyzers and
index configurations for the specified cluster.

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

The following table shows the modes of access each role supports.

Role

|

Action

|

Atlas UI

|

Atlas API

|

Atlas Search API

|

Atlas CLI  
  
|||||  
  
`Project Data Access Read Only` or higher role

|

To view Atlas Search analyzers and indexes.

|

✓

|

✓

|

|  
  
`Project Data Access Admin` or higher role

|

To create and manage Atlas Search analyzers and indexes, and assign the role
to your API Key.

|

✓

|

✓

|

✓

|

✓  
  
`Project Owner` role

|

To create and assign project access to API Keys.

|

|

|

✓

|

✓  
  
`Organization Owner` role

|

To create access list entries for your API Key and send the request from a
client that appears in the access list for your API Key.

|

|

|

✓

|

✓  
  
`Project Search Index Editor`

|

To create, view, edit, and delete Atlas Search indexes using the Atlas UI or
API.

|

✓

|

✓

|

✓

|  
  
## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    DELETE /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes/{INDEX-ID}  
      
  
## Request Parameters

### Request Path Parameters

Path Element

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

Unique identifier for the project that contains the specified cluster.  
  
`CLUSTER-NAME`

|

string

|

Required

|

Name of the cluster containing the database and collection with one or more
Atlas Search indexes.  
  
`INDEX-ID`

|

string

|

Required

|

Unique identifier of the Atlas Search index. Use the Get All Atlas Search
Indexes for a Collection API endpoint to find the IDs of all Atlas Search
indexes.  
  
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

## Response Elements

This endpoint does not have response elements.

## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Content-Type: application/json" \  
         --include \  
         --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes/{INDEX-ID}?pretty=true"  
  
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

