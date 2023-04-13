Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Private Endpoint Service for One Provider

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

Retrieve details for one private endpoint service for AWS, Azure, or Google
Cloud in an Atlas project.

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

    
    
    GET /groups/{GROUP-ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService/{ENDPOINT-SERVICE-ID}  
      
  
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

Unique identifier for the project that contains the private endpoint service
that you want to retrieve.  
  
{CLOUD-PROVIDER}

|

string

|

Required

|

Cloud provider for which you want to retrieve a private endpoint service.
Atlas accepts **AWS** , **AZURE** , or **GCP**.  
  
{ENDPOINT-SERVICE-ID}

|

string

|

Required

|

Unique identifier of the private endpoint service that you want to retrieve.  
  
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

AWS

Azure

GCP

Response Parameter

|

Type

|

Description  
  
||  
  
endpointServiceName

|

string

|

Name of the AWS PrivateLink endpoint service. Atlas returns `null` while it is
creating the endpoint service.  
  
errorMessage

|

string

|

Error message pertaining to the AWS PrivateLink connection. Returns `null` if
there are no errors.  
  
id

|

string

|

Unique identifier of the AWS PrivateLink connection.  
  
interfaceEndpoints

|

array of strings

|

Unique identifiers of the interface endpoints in your VPC that you added to
the AWS PrivateLink connection.  
  
status

|

string

|

Status of the AWS PrivateLink connection. Atlas returns one of the following
values:

|

Status

|

Description  
  
|  
  
INITIATING

|

Atlas is creating the network load balancer and VPC endpoint service.  
  
WAITING_FOR_USER

|

The Atlas network load balancer and VPC endpoint service are created and ready
to receive connection requests.

When you receive this status, create an interface endpoint to continue
configuring the AWS PrivateLink connection.  
  
FAILED

|

A system failure has occurred.  
  
DELETING

|

The AWS PrivateLink connection is being deleted.  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService/{ENDPOINT-SERVICE-ID}?pretty=true"  
  
## Example Response

AWS

Azure

GCP

    
    
    1| {  
    |  
    2|   "endpointServiceName": "com.amazonaws.vpce.us-east-1.vpce-svc-0afd34ee97e30d43f",  
    3|   "errorMessage": null,  
    4|   "id": "5f7cac1adf5d6c6306f4b283",  
    5|   "interfaceEndpoints": [],  
    6|   "status": "WAITING_FOR_USER"  
    7| }  
  
What is MongoDB Atlas? →

