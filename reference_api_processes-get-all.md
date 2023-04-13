Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All MongoDB Processes in a Group

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Response Document
  * results Embedded Document
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

Get all Atlas MongoDB processes for the specified project. An Atlas MongoDB
process can be either a `mongod` or a `mongos`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET api/atlas/v1.0/groups/{GROUP-ID}/processes  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required.

|

The unique identifier for the project whose MongoDB processes you want to
retrieve.  
  
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

## Response Elements

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
  
links

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
## Example Request

## Important

You must modify the following code block with the appropriate credentials and
project ID.

    
    
    curl -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/processes?pretty=true"  
      
  
## Example Response

    
    
    {  
      
      "links" : [ ... ],  
      "results" : [ {  
        "created" : "2020-08-25T18:44:13Z",  
        "groupId" : "12345678",  
        "hostname" : "atlas-abcdef-shard-00-00.nta8e.mongodb.net",  
        "id" : "atlas-abcdef-shard-00-00.nta8e.mongodb.net:27017",  
        "lastPing" : "2020-09-01T18:40:06Z",  
        "links" : [ ... ],  
        "port" : 27017,  
        "replicaSetName" : "atlas-abcdef-shard-0",  
        "typeName" : "REPLICA_PRIMARY",  
        "userAlias" : "testcluster-shard-00-00.nta8e.mongodb.net"  
        "version" : "4.4.0"  
      },  
      ...  
      ],  
      "totalCount" : 6  
    }  
  
What is MongoDB Atlas? →

