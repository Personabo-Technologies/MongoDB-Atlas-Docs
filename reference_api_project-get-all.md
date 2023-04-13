Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Projects

Share Feedback

On this page

  * Syntax
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

    
    
    GET /groups  
      
  
### Request Query Parameters

This endpoint may use any of the HTTP request query parameters available to
all Atlas Administration API resources. These are all optional.

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
  
pageNum

|

integer

|

Optional

|

Page number, starting with one, that Atlas returns of the total number of
objects.

|

`1`  
  
itemsPerPage

|

integer

|

Optional

|

Number of items that Atlas returns per page, up to a maximum of 500.

|

`100`  
  
includeCount

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the **totalCount** parameter in the
response body.

|

`true`  
  
pretty

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the JSON response in the prettyprint
format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag that indicates whether Atlas wraps the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

Endpoints that return a list of results use the **results** object as an
envelope. Atlas adds the **status** parameter to the response body.

|

`false`  
  
### HTTP Response Elements

If you set the query element `envelope` to `true`, the response is wrapped by
the `content` object.

The HTTP response returns a JSON document that includes the following objects:

#### `results`

An array of documents, each representing one Atlas project.

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

An array of documents, representing a link to one or more sub-resources and/or
related resources, such as list pagination. See Linking for more information.  
  
`name`

|

The name of the project. You can use this value for populating the `{GROUP-
NAME}` parameter of the /groups/byName/{GROUP-NAME} endpoint.  
  
`orgId`

|

The unique identifier of the Atlas organization to which the project belongs.  
  
#### `links`

An array of documents, representing a link to one or more sub-resources and/or
related resources such as list pagination. See Linking for more information.

#### `totalCount`

The total number of items in the result set. This value may be higher than the
number of objects in the `results` array if the entire result set is
paginated.

## Example

### Request

    
    
    curl -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups"  
      
  
### Response

    
    
    HTTP/1.1 200 OK  
      
      
    {  
      "links" : [ {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups",  
        "rel" : "self"  
      } ],  
      "results" : [ {  
        "clusterCount" : 2,  
        "created" : "2016-07-14T14:19:33Z",  
        "id" : "5a0a1e7e0f2912c554080ae6",  
        "links" : [ {  
          "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/5a0a1e7e0f2912c554080ae6",  
          "rel" : "self"  
        } ],  
        "name" : "ProjectBar",  
        "orgId" : "5a0a1e7e0f2912c554080adc"  
      }, {  
        "clusterCount" : 0,  
        "created" : "2017-10-16T15:24:01Z",  
        "id" : "5a0a1e7e0f2912c554080ae7",  
        "links" : [ {  
          "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/5a0a1e7e0f2912c554080ae7",  
          "rel" : "self"  
        } ],  
        "name" : "Project Foo",  
        "orgId" : "5a0a1e7e0f2912c554080adc"  
      } ],  
      "totalCount" : 2  
    }  
  
What is MongoDB Atlas? →

