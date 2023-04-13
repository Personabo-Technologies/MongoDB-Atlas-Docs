Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Private Endpoint Service for One Provider

Share Feedback

On this page

  * Considerations
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

Create one private endpoint service for AWS, Azure, or Google Cloud in an
Atlas project.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Considerations

  * When you create a private endpoint service, Atlas creates a network container in the project for the cloud provider for which you create the private endpoint service if one does not already exist.

## Required Roles

You must have at the `Project Owner` role for the project to successfully call
this resource.

## Request

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/privateEndpoint/endpointService  
      
  
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

Unique identifier for the project for which you want to create a private
endpoint service.  
  
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
  
providerName

|

string

|

Required

|

Name of the cloud provider for which you want to create the private endpoint
service. Atlas accepts **AWS** , **AZURE** , or **GCP**.  
  
region

|

string

|

Required

|

Cloud provider region for which you want to create the private endpoint
service. To learn which values Atlas accepts for each cloud provider, see:

  * Amazon Web Services (AWS)

  * Microsoft Azure

  * Google Cloud Platform (GCP)

## Important

Some Atlas clusters on Azure created before 10/16/2020 use Azure networking
hardware that is incompatible with Azure Private Link. You can still configure
Azure Private Link for Atlas projects with these clusters to use with
supported clusters in the project, but you will not be able to connect to the
incompatible ones through Azure Private Link.

All new Atlas clusters are compatible with Azure Private Link. If you must
connect to your cluster using only Azure Private Link, you can create a new
cluster in the same Atlas project and migrate your data.  
  
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

AWS

Azure

GCP

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/endpointService?pretty=true" \  
    5|      --data '  
    6|        {  
    7|          "providerName" : "AWS",  
    8|          "region" : "us-east-1"  
    9|        }'  
  
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

