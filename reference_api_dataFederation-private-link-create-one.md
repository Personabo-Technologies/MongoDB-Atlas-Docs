Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Add One Private Endpoint

Share Feedback

On this page

  * Permissions Required
  * Resources
  * Syntax
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * `links` Array
  * `results` Array
  * `totalCount` Document
  * Examples
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

You can add an AWS private endpoint for the federated database instances in
the project from the API. When you submit this request through the API:

  * If the endpoint ID already exists and there is no change to the associated comment, Atlas Data Federation makes no change to the endpoint ID list.

  * If the endpoint ID already exists and there is a change to the associated comment, Atlas Data Federation updates the `comment` value only in the endpoint ID list.

  * If the endpoint ID doesn't exist, Atlas Data Federation appends the new endpoint to the list of endpoints in the endpoint ID list.

The following table shows the service names for the various endpoints in each
region:

Region

|

Service Name  
  
|  
  
`us-east-1`

|

`com.amazonaws.vpce.us-east-1.vpce-svc-00e311695874992b4`  
  
`us-west-1`

|

`com.amazonaws.vpce.us-west-2.vpce-svc-09d86b19e59d1b4bb`  
  
`eu-west-1`

|

`com.amazonaws.vpce.eu-west-1.vpce-svc-0824460b72e1a420e`  
  
`eu-west-2`

|

`com.amazonaws.vpce.eu-west-2.vpce-svc-052f1840aa0c4f1f9`  
  
`eu-central-1`

|

`com.amazonaws.vpce.eu-central-1.vpce-svc-0ac8ce91871138c0d`  
  
`sa-east-1`

|

`com.amazonaws.vpce.sa-east-1.vpce-svc-0b56e75e8cdf50044`  
  
`ap-southeast-2`

|

`com.amazonaws.vpce.ap-southeast-2.vpce-svc-036f1de74d761706e`  
  
`ap-south-1`

|

`com.amazonaws.vpce.ap-south-1.vpce-svc-03eb8a541f96d356d`  
  
The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Permissions Required

You must have the `GROUP_ATLAS_ADMIN` (`Project Owner`) role to create a
private endpoint.

## Resources

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /groups/{GROUP-ID}/privateNetworkSettings/endpointIds  
      
  
## Request Parameters

### Request Path Parameters

Path Element

|

Necessity

|

Description  
  
||  
  
`GROUP-ID`

|

Required

|

Unique 24-digit hexadecimal string that identifies the project.  
  
### Request Query Parameters

The following query parameters are optional:

Query Parameter

|

Type

|

Description

|

Default  
  
|||  
  
`pretty`

|

boolean

|

Displays response in a prettyprint format.

|

`false`  
  
`envelope`

|

boolean

|

Specifies whether or not to wrap the response in an envelope.

|

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
  
`comment`

|

string

|

Optional

|

Human-readable string to associate with this private endpoint.  
  
`endpointId`

|

string

|

Required

|

Unique 22-character alphanumeric string that identifies the private endpoint.
Atlas Data Federation supports AWS private endpoints using the AWS PrivateLink
feature.  
  
`provider`

|

string

|

Required

|

Human-readable label that identifies the cloud provider of this endpoint.
Atlas Data Federation supports AWS only. If empty, defaults to AWS.  
  
`type`

|

string

|

Required

|

Human-readable label that identifies the type of resource to associate with
this private endpoint. Value must be `DATA_LAKE`. If empty, defaults to
`DATA_LAKE`.  
  
## Response Elements

### `links` Array

The `links` array includes one or more links to sub-resources or related
resources. The relations between URLs are explained in the Web Linking
Specification.

Relation

|

Description  
  
|  
  
`self`

|

The URL endpoint for this resource.  
  
### `results` Array

Each element in the `result` array is one private endpoint.

Name

|

Type

|

Description  
  
||  
  
`comment`

|

string

|

Human-readable string associated with this private endpoint.  
  
`endpointId`

|

string

|

Unique 22-character alphanumeric string that identifies the private endpoint.
Atlas Data Federation supports AWS private endpoints using the AWS PrivateLink
feature.  
  
`provider`

|

string

|

Human-readable label that identifies the cloud provider for this endpoint.
Value is AWS.  
  
`type`

|

string

|

Human-readable label that identifies the resource associated with this private
endpoint. Value is `DATA_LAKE`.  
  
### `totalCount` Document

This value is the count of the total number of items in the result set.
`totalCount` may be greater than the number of objects in the `results` array
if the entire result set is paginated.

## Examples

### Request

## Example

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
       --header "Accept: application/json" \  
       --header "Content-Type: application/json" \  
       --include \  
       --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateNetworkSettings/endpointIds?pretty=true" \  
       --data '  
       {  
         "endpointId" : "vpce-jjg5e24qp93513h03",  
         "type": "DATA_LAKE",  
         "provider": "AWS",  
         "comment" : "Private endpoint for Application Server A"  
       }'  
  
### Response

## Example

    
    
    {  
      
      "links" : [ {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateNetworkSettings/endpointIds?pretty=true&pageNum=1&itemsPerPage=100",  
        "rel" : "self"  
      } ],  
      "results" : [ {  
        "comment" : "Private endpoint for Application Server A",  
        "endpointId" : "vpce-jjg5e24qp93513h03",  
        "provider" : "AWS",  
        "type" : "DATA_LAKE"  
      } ],  
      "totalCount" : 1  
    }  
  
What is MongoDB Atlas? →

