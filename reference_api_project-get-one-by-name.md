Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Project by Name

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * HTTP Response Elements
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/byName/{GROUP-NAME}  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`GROUP-NAME`

|

Required.

|

The name of the project whose information you want to retrieve.  
  
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
  
### HTTP Response Elements

If you set the query element `envelope` to `true`, the response is wrapped by
the `content` object.

The HTTP response returns a JSON document that includes the following objects:

Name

|

Description  
  
|  
  
`clusterCount`

|

The number of Atlas clusters deployed in the project.  
  
`created`

|

The ISO-8601-formatted timestamp of when Atlas created the project.  
  
`id`

|

The unique identifier of the project. You can use this value for populating
the `{GROUP-ID}` parameter of other Atlas Administration API endpoints.  
  
`links`

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
`name`

|

The name of the project. You can use this value for populating the `{GROUP-
NAME}` parameter of the /groups/byName/{GROUP-NAME} endpoint.  
  
`orgId`

|

The unique identifier of the Atlas organization to which the project belongs.  
  
## Example

### Request

    
    
    curl -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/byName/ProjectBar"  
      
  
### Response

    
    
     HTTP/1.1 200 OK  
      
      
     {  
       "clusterCount" : 2,  
       "created" : "2016-07-14T14:19:33Z",  
       "id" : "5a0a1e7e0f2912c554080ae6",  
       "links" : [],  
       "name" : "ProjectBar",  
       "orgId" : "5a0a1e7e0f2912c554080adc"  
    }  
  
What is MongoDB Atlas? →

