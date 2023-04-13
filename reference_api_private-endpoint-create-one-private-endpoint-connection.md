Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Private Endpoint Connection

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

Create one private endpoint connection in an Atlas project.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Considerations

  * When you create a private endpoint connection, Atlas creates a network container in the project for the cloud provider for which you create the private endpoint connection if one does not already exist.

### Required Roles

You must have one of the following roles to successfully call this resource:

  * `Organization Owner`

  * `Project Owner`

### Request

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/privateEndpoint  
      
  
## Request Path Parameters

Parameter

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
  
## Request Query Parameters

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
  
## Request Body Parameters

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`providerName`

|

string

|

Required

|

Name of the cloud provider you want to create the private endpoint connection
for.

Must be `AWS`.  
  
`region`

|

string

|

Required

|

Cloud provider region in which you want to create the private endpoint
connection. Accepted values are:

  * `us-east-1`

  * `us-east-2`

  * `us-west-1`

  * `us-west-2`

  * `ca-central-1`

  * `sa-east-1`

  * `eu-north-1`

  * `eu-west-1`

  * `eu-west-2`

  * `eu-west-3`

  * `eu-central-1`

  * `me-south-1`

  * `ap-northeast-1`

  * `ap-northeast-2`

  * `ap-south-1`

  * `ap-southeast-1`

  * `ap-southeast-2`

  * `ap-east-1`

  
  
### Response Elements

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
  
### Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|   --header "Accept: application/json" \  
    3|   --header "Content-Type: application/json" \  
    4|   --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/?pretty=true" \  
    5|   --data '  
    6|     {  
    7|       "providerName":"AWS",  
    8|       "region":"us-east-1"  
    9|     }'  
  
### Example Response

    
    
    1| {  
    |  
    2|   "endpointServiceName": "com.amazonaws.vpce.us-east-1.vpce-svc-0aee615d3fe32c14e",  
    3|   "errorMessage": null,  
    4|   "id": "5df264b8f10fab7d2cad2f0d",  
    5|   "interfaceEndpoints": ["vpce-08fb7e9319909ec7b"],  
    6|   "status": "WAITING_FOR_USER"  
    7| }  
  
What is MongoDB Atlas? →

