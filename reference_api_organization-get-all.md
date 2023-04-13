Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Organizations

Share Feedback

On this page

  * Resource
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

    
    
    GET /orgs  
      
  
### Request Path Parameters

This endpoint does not use HTTP request path parameters.

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

Organization name with which to filter the returned list. Performs a case-
insensitive search for organizations which exactly match the specified `name`.

## Example

If you specify a `name` query parameter of `org1`, Atlas returns organizations
named `org1` and `Org1`, but would not return an organization named `org123`.

|  
  
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

Each element in the `result` array is one organization.

Name

|

Type

|

Description  
  
||  
  
`id`

|

ObjectId

|

Unique identifier for the organization.  
  
`isDeleted`

|

boolean

|

Flag indicating if the organization is deleted.  
  
`name`

|

string

|

Name of the organization.  
  
`links`

|

document array

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
## Example Request

    
    
    curl --include --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
      --header "Accept: application/json" \  
      --header "Content-Type: application/json" \  
      "https://cloud.mongodb.com/api/atlas/v1.0/orgs?pretty=true"  
  
## Example Response

    
    
    {  
      
      "links" : [  
         {  
           "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs",  
           "rel" : "self"  
         }  
      ],  
      "results" : [  
         {  
           "id" : "5a2add1cfd9f3cfb17053317",  
           "isDeleted": false,  
           "links": [{  
              "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5a2add1cfd9f3cfb17053317",  
              "rel": "self"  
         }],  
           "name" : "Internal Application Support"  
         },  
         {  
           "id" : "5a2add1cfd9f3cfb17053318",  
           "isDeleted": false,  
           "links": [{  
              "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5a2add1cfd9f3cfb17053318",  
              "rel": "self"  
         }],  
           "name" : "Customer Application Support"  
         },  
         {  
           "id" : "5a2add1cfd9f3cfb17053319",  
           "isDeleted": false  
           "links": [{  
              "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5a2add1cfd9f3cfb17053319",  
              "rel": "self"  
         }],  
           "name" : "Research and Development"  
         }  
      ],  
      "totalCount" : 3  
    }  
  
What is MongoDB Atlas? →

