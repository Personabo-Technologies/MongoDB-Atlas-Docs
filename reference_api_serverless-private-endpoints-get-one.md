Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return One Private Endpoint for One Serverless Instance

Share Feedback

On this page

  * Required Roles
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

Return details for one private endpoint for one Atlas serverless instance.
Serverless instances support private endpoints on AWS only.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You must have at least the `Project Read Only` role for the project to
successfully call this resource.

## Request

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/privateEndpoint/serverless/instance/  
      
    {INSTANCE-NAME}/endpoint/{ENDPOINT-ID}  
  
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

Human-readable label that identifies the serverless instance associated with
the tenant endpoint.  
  
{ENDPOINT-ID}

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the tenant endpoint.  
  
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

Human-readable statement associated with the private endpoint.  
  
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

Human-readable error message that indicates the error condition associated
with establishing the private endpoint connection.  
  
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
    3|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/serverless/instance/  
    4|      {INSTANCE-NAME}/endpoint/{ENDPOINT-ID}?pretty=true"  
  
## Example Response

    
    
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

