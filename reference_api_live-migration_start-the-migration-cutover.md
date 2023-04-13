Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Start the Migration Cutover

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

Start the push live migration cutover stage and confirm when the cutover stage
completes. When the cutover stage completes, the push live migration process
stops synchronizing with the source cluster and the live migration job
completes migration.

## Required Roles

Your API Key must have the `Organization Owner` role to successfully call this
resource.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    PUT /groups/{groupId}/liveMigrations/{liveMigrationId}/cutover  
      
  
### Request Path Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
groupId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies your project.  
  
liveMigrationId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the live migration job.  
  
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

Name

|

Type

|

Description  
  
||  
  
_id

|

string

|

Unique 24-hexadecimal digit string that identifies this process validating the
live migration.  
  
groupId

|

string

|

Unique 24-hexadecimal digit string that identifies the Atlas project to
validate.  
  
status

|

string

|

State of the validation job when you submitted this request. Returns
`"PENDING"`, `"SUCCESS"`, or `"FAILED"`.  
  
sourceGroupId

|

string

|

Unique 24-hexadecimal digit string that identifies the source (Cloud Manager
or Ops Manager) project.  
  
errorMessage

|

string

|

Reason why the validation job failed.  
  
## Example Request

    
    
    curl --user '{USERNAME}:{APIKEY}' --digest \  
      
         --header 'Accept: application/json' \  
         --header 'Content-Type: application/json' \  
         --include \  
         --request PUT 'https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/liveMigrations/{liveMigrationId}/cutover?pretty=true'  
  
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
      
      "_id": "a659ce44c03ca1e348b1e992",  
      "groupId": "7e68e12770616e75e6df43d0",  
      "sourceGroupId": "7e68e12770616e75e6df43d0",  
      "status": "PENDING"  
    }  
  
What is MongoDB Atlas? →

