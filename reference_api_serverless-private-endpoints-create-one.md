Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Private Endpoint for One Serverless Instance

Share Feedback

On this page

  * Required Roles
  * Resource
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

Creates one private endpoint for one Atlas serverless instance. Serverless
instances support private endpoints on AWS only.

## Important

After you create the private endpoint in Atlas, you must complete additional
steps to make it available for use. To learn more, see the Atlas
Administration API tab on Set Up a Private Endpoint for a Serverless Instance.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You must have at the `Project Owner` role for the project to successfully call
this resource.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/privateEndpoint/serverless/instance/  
      
    {INSTANCE-NAME}/endpoint  
  
## Request

### Request Path Parameters

Path Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
{GROUP-ID}

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies your project.  
  
{INSTANCE-NAME}

|

string

|

Required

|

Human-readable label that identifies the serverless instance for which the
tenant endpoint will be created.  
  
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

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
comment

|

string

|

Optional

|

Human-readable comment associated with the private endpoint. The comment must
be less than 80 characters.  
  
## Response

Response Parameter

|

Type

|

Description  
  
||  
  
_id

|

string

|

Unique 24-hexadecimal digit string that identifies the private endpoint.  
  
cloudProviderEndpointId

|

string

|

Unique string that identifies the private endpoint's network interface.  
  
comment

|

string

|

Human-readable comment associated with the private endpoint. The comment must
be less than 80 characters.  
  
endpointServiceName

|

string

|

Unique string that identifies the PrivateLink endpoint service. MongoDB Cloud
returns `null` while it creates the endpoint service.  
  
errorMessage

|

string

|

Human-readable error message that indicates error condition associated with
establishing the private endpoint connection.  
  
status

|

string

|

Human-readable label that indicates the current operating status of the
private endpoint. Values include: `RESERVATION_REQUESTED`, `RESERVED`,
`INITIATING`, `AVAILABLE`, `FAILED`, `DELETING`.  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/serverless/instance/{INSTANCE-NAME}/endpoint?pretty=true" \  
    5|      --data '  
    6|        {  
    7|          "comment" : "example comment"  
    8|        }'  
  
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

    
    
    1| {  
    |  
    2|   "_id": "5f7cac1adf5d6c6306f4b283",  
    3|   "cloudProviderEndpointId": "vpce-fcac938279cd98dc894",  
    4|   "comment": "example comment",  
    5|   "endpointServiceName": "com.amazonaws.vpce.us-east-1.vpce-svc-0afd34ee97e30d43f",  
    6|   "errorMessage": null,  
    7|   "status": "AVAILABLE"  
    8| }  
  
What is MongoDB Atlas? →

