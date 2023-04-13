Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Teams

Share Feedback

On this page

  * Syntax
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

## Syntax

    
    
    GET /orgs/{ORG-ID}/teams  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`ORG-ID`

|

Required.

|

The unique identifier for the organization whose teams you want to retrieve.  
  
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

Each element in the `result` array is one team.

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

Unique identifier for the team.  
  
`name`

|

string

|

Name of the team.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest -i \  
      
      --header "Accept: application/json" \  
      --header "Content-Type: application/json" \  
      "https://cloud.mongodb.com/api/atlas/v1.0/orgs/7253g4s820thk69bfecd7bv1/teams?pretty=true"  
  
## Example Response

    
    
    {  
      
            "links": [{  
                   "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/7253g4s820thk69bfecd7bv1/teams?pageNum=1&itemsPerPage=100",  
                   "rel": "self"  
            }],  
            "results": [{  
                    "id": "b5cfec387d9d63926b9189g",  
                    "name": "Finance"  
            }, {  
                    "id": "6b610e4f80eef5366613e4df",  
                    "name": "Research and Development"  
            }, {  
                    "id": "6b610e1087d9d66b272f0c86",  
                    "name": "Technical Documentation"  
            }],  
            "totalCount": 3  
    }  
  
What is MongoDB Atlas? →

