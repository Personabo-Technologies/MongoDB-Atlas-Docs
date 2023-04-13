Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Link-Token

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

Create one new link-token. Atlas uses the link-token for push live migrations
only. Live migration (push) allows you to securely push data from Cloud
Manager or Ops Manager into Atlas. To learn more, see the list of tools for
migrating to Atlas.

## Required Roles

Your API Key must have the `Organization Owner` role to successfully call this
resource.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /orgs/{orgId}/liveMigrations/linkTokens  
      
  
### Request Path Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
orgId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the destination (Atlas)
organization that contains your projects.  
  
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

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
accessListIps

|

array

|

Required

|

One IP address access list entry associated with the API key.  
  
## Response

Name

|

Type

|

Description  
  
||  
  
linkToken

|

string

|

Atlas-generated token that links the source (Cloud Manager or Ops Manager) and
destination (Atlas) clusters for migration.  
  
## Example Request

    
    
    curl --user '{USERNAME}:{APIKEY}' --digest \  
      
         --header 'Accept: application/json' \  
         --header 'Content-Type: application/json' \  
         --include \  
         --request POST 'https://cloud.mongodb.com/api/atlas/v1.0/orgs/{orgId}/liveMigrations/linkTokens?pretty=true' \  
         --data '{  
             "accessListIps": [  
               "string"  
             ]  
           }'  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 201 Created  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    {  
      
      "linkToken": [  
        "string"  
      ]  
    }  
  
What is MongoDB Atlas? →

