Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Organization

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

    
    
    GET /orgs/{ORG-ID}  
      
  
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

The unique identifier for the Atlas organization whose information you want to
retrieve.  
  
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
      "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}?pretty=true"  
  
## Example Response

    
    
     {  
      
       "id" : "5a2add1cfd9f3cfb17053318",  
       "isDeleted": false,  
       "links": [{  
      "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5a2add1cfd9f3cfb17053318",  
      "rel": "self"  
    }, {  
      "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5a2add1cfd9f3cfb17053318/groups",  
      "rel": "http://mms.mongodb.com/groups"  
    }, {  
      "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5a2add1cfd9f3cfb17053318/teams",  
      "rel": "http://mms.mongodb.com/teams"  
    }, {  
      "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5a2add1cfd9f3cfb17053318/users",  
      "rel": "http://mms.mongodb.com/users"  
    }],  
       "name" : "Customer Application Support"  
     }  
  
What is MongoDB Atlas? →

