Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Private Endpoint for One Provider

Share Feedback

On this page

  * Prerequisites
  * Create a private endpoint service.
  * Create the private endpoint.
  * Create a private endpoint service.
  * Disable the private endpoint policies.
  * Create the private endpoint.
  * Create a private endpoint service.
  * Create the private endpoints in Google Cloud.
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

Create one of the following:

  * One private endpoint for AWS or Azure in an Atlas project.

  * One private endpoint group for Google Cloud in an Atlas project. Endpoint groups represent a collection of endpoints. To learn more, see Set up a Private Endpoint.

If the attempt to add an endpoint or endpoint group fails, delete it, then try
to add a new one.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Prerequisites

You must complete the following steps for your cloud provider before you can
create a private endpoint or endpoint group:

AWS

Azure

GCP

1

### Create a private endpoint service.

Create One Private Endpoint Service for One Provider in the AWS region to
which you want to deploy your private endpoint.

2

### Create the private endpoint.

Create the endpoint in AWS with the following information:

  * The unique identifier of the peer AWS VPC.

  * The unique identifiers of the subnets your AWS VPC uses.

  * The endpoint service that you created with /groups/{GROUP-ID}/privateEndpoint/endpointService.

Retrieve the endpoint service name with /groups/{GROUP-
ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService/{ENDPOINT-SERVICE-ID}.

Note the **VpcEndpointId** in the response from the `CreateVpcEndpoint` AWS
CLI command. Include the value of this field as the **id** in the request body
for /groups/{GROUP-ID}/privateEndpoint/{CLOUD-
PROVIDER}/endpointService/{ENDPOINT-SERVICE-ID}/endpoint.

## Required Roles

You must have at the `Project Owner` role for the project to successfully call
this resource.

## Request

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/privateEndpoint/{CLOUD-PROVIDER}/endpointService/{ENDPOINT-SERVICE-ID}/endpoint  
      
  
### Request Path Parameters

Path Parameter

|

Type

|

Necessity

|

Descriptionon  
  
|||  
  
{GROUP-ID}

|

string

|

Required

|

Unique identifier for the project for which you want to create a private
endpoint.  
  
{CLOUD-PROVIDER}

|

string

|

Required

|

Cloud provider for which you want to create a private endpoint. Atlas accepts
**AWS** , **AZURE** , or **GCP**.  
  
{ENDPOINT-SERVICE-ID}

|

string

|

Required

|

Unique identifier of the private endpoint service for which you want to create
a private endpoint.  
  
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

AWS

Azure

GCP

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
id

|

string

|

Required

|

Unique identifier of the private endpoint you created in your AWS VPC.  
  
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

AWS

Azure

GCP

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/AWS/endpointService/{ENDPOINT-SERVICE-ID}/endpoint?pretty=true" \  
    5|      --data '  
    6|        {  
    7|          "id" : "vpce-0d00c26273372c6ef"  
    8|        }'  
  
## Example Response

AWS

Azure

GCP

    
    
    1| {  
    |  
    2|   "connectionStatus": "PENDING",  
    3|   "deleteRequested": false,  
    4|   "errorMessage": null,  
    5|   "interfaceEndpointId": "vpce-08fb7e9319909ec7b"  
    6| }  
  
What is MongoDB Atlas? →

