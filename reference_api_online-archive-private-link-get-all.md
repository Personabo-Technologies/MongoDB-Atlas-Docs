Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Private Endpoints

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
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

You can retrieve all the AWS private endpoints for the online archives in the
project from the API.

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

You must have the `GROUP_READ_ONLY` (`Project Data Access Read Only`) or
higher role to retrieve private endpoints for the online archives.

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

This endpoint does not use HTTP request body parameters.

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

Unique 22-character alphanumeric string that identifies this private endpoint.  
  
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

Human-readable label that identifies the type of resource associated with this
private endpoint. Value is `DATA_LAKE`.  
  
### `totalCount` Document

This value is the count of the total number of items in the result set.
`totalCount` may be greater than the number of objects in the `results` array
if the entire result set is paginated.

## Example

### Request

## Example

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
       --header "Accept: application/json" \  
       --header "Content-Type: application/json" \  
       --include \  
       --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateNetworkSettings/endpointIds?pretty=true"  
  
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

