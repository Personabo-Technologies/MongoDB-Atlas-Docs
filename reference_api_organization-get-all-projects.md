Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Projects in an Organization

Share Feedback

On this page

  * Resource
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /orgs/{ORG-ID}/groups  
      
  
## Request Parameters

### Request Path Parameters

Path Element

|

Type

|

Necessity

|

Description  
  
|||  
  
ORG-ID

|

string

|

Required

|

Unique 24-hexadecimal-digit string that identifies the organization whose
information you want to retrieve.  
  
### Request Query Parameters

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
  
|

|

|

|  
  
||||  
  
name

|

string

|

Optional

|

Project name with which to filter the returned list. Performs a case-
insensitive search search for a project within the organization which exactly
match the specified `name`.

## Example

If you specify a `name` query parameter of `project1`, Atlas returns the
project named `project1`, but would not return a project named `project123`.

|

None  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

### Response Document

The response JSON document includes an array of **result** objects, an array
of **link** objects and a count of the total number of **result** objects
retrieved.

Name

|

Type

|

Description  
  
||  
  
results

|

array of objects

|

One object for each item detailed in the results Embedded Document section.  
  
links

|

array of objects

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
totalCount

|

integer

|

Count of the total number of items in the result set. It may be greater than
the number of objects in the **results** array if the entire result set is
paginated.  
  
### results Embedded Document

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

An array of documents. Contains a link to the following resource:

  * `/api/atlas/v1.0/groups/{GROUP-ID}/`

A self-referential link to the project.

  
  
`name`

|

The name of the project. You can use this value for populating the `{GROUP-
NAME}` parameter of the /groups/byName/{GROUP-NAME} endpoint.  
  
`orgId`

|

The unique identifier of the Atlas organization to which the project belongs.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/groups"  
  
## Example Response

    
    
    {  
      
     "links": [  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5a0a1e7e0f2912c554080adc/groups?pageNum=1&itemsPerPage=100",  
             "rel": "self"  
         }  
     ],  
     "results": [  
         {  
             "clusterCount": 1,  
             "created": "2018-02-02T00:32:31Z",  
             "id": "5ad645d4806d0119d6b35638",  
             "links": [  
                 {  
                     "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5ad645d4806d0119d6b35638",  
                     "rel": "self"  
                 }  
             ],  
             "name": "Production",  
             "orgId": "5a0a1e7e0f2912c554080adc"  
         },  
         {  
             "clusterCount": 1,  
             "created": "2017-02-06T17:59:05Z",  
             "id": "5ad645d4806d0119d6b35639",  
             "links": [  
                 {  
                     "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5ad645d4806d0119d6b35639",  
                     "rel": "self"  
                 }  
             ],  
             "name": "Staging",  
             "orgId": "5a0a1e7e0f2912c554080adc"  
         }  
     ],  
     "totalCount": 2  
    }  
  
What is MongoDB Atlas? →

