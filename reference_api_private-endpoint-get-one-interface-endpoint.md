Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Interface Endpoint by ID

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

Retrieve one interface endpoint in a private endpoint connection in an Atlas
project.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You must have one of the following roles to successfully call this resource:

  * `Organization Owner`

  * `Project Owner`

## Request

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/privateEndpoint/{privateLinkId}/interfaceEndpoints/{interfaceEndpointId}  
      
  
### Request Path Parameters

Path Parameter

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
  
`privateLinkId`

|

Required

|

Unique identifier of the AWS PrivateLink connection.  
  
`interfaceEndpointId`

|

string

|

Unique identifier of the interface endpoint.  
  
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
  
connectionStatus

|

string

|

Status of the interface endpoint. Returns one of the following values:

|

Status

|

Description  
  
|  
  
NONE

|

Atlas created the network load balancer and VPC endpoint service, but AWS
hasn't yet created the VPC endpoint.  
  
PENDING_ACCEPTANCE

|

AWS has received the connection request from your VPC endpoint to the Atlas
VPC endpoint service.  
  
PENDING

|

AWS is establishing the connection between your VPC endpoint and the Atlas VPC
endpoint service.  
  
AVAILABLE

|

Atlas VPC resources are connected to the VPC endpoint in your VPC. You can
connect to Atlas clusters in this region using AWS PrivateLink.  
  
REJECTED

|

AWS failed to establish a connection between Atlas VPC resources to the VPC
endpoint in your VPC.  
  
DELETING

|

Atlas is removing the interface endpoint from the private endpoint connection.  
  
deleteRequested

|

boolean

|

Flag that indicates whether Atlas received a request to remove the interface
endpoint from the private endpoint connection.  
  
errorMessage

|

string

|

Error message pertaining to the interface endpoint. Atlas returns **null** if
there are no errors.  
  
interfaceEndpointId

|

string

|

Unique identifier of the interface endpoint.  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|   --header "Accept: application/json" \  
    3|   --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/{privateLinkId}/interfaceEndpoints/{interfaceEndpointId}?pretty=true"  
  
## Example Response

    
    
    1| {  
    |  
    2|   "connectionStatus": "PENDING",  
    3|   "deleteRequested": false,  
    4|   "errorMessage": null,  
    5|   "interfaceEndpointId": "vpce-08fb7e9319909ec7b"  
    6| }  
  
What is MongoDB Atlas? →

