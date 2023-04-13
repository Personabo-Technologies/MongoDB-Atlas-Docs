Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get X.509 Certificates for a User

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request
  * Path Parameters
  * Query Parameters
  * Body Parameters
  * Response
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Get a list of all Atlas-managed, unexpired certificates for a database user.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Required Roles

You must have the `Atlas admin` role to use this endpoint.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/databaseUsers/{USERNAME}/certs  
      
  
## Request

### Path Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`GROUP-ID`

|

string

|

Required

|

Identifier for the Atlas project associated with the X.509 configuration.  
  
`USERNAME`

|

string

|

Required

|

Username of the database user to get certificates for.  
  
### Query Parameters

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
  
### Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
`links`

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
`results`

|

array of objects

|

Array of objects where each details one unexpired database user certificate.  
  
`results[n]._id`

|

number

|

Serial number of this certificate.  
  
`results[n].createdAt`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas created this
X.509 certificate.  
  
`results[n].groupId`

|

string

|

Unique identifier of the Atlas project to which this certificate belongs.  
  
`results[n].notAfter`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when this certificate
expires.  
  
`results[n].subject`

|

string

|

Fully distinguished name of the database user to which this certificate
belongs. To learn more, see RFC 2253.  
  
`totalCount`

|

number

|

Total number of unexpired certificates returned in this response.  
  
## Example

### Request

The following example returns a list of all Atlas-managed, unexpired
certificates for a database user, along with a total count of those
certificates.

    
    
    curl --request GET \  
      
     --user "{publicApiKey}:{privateApiKey}" \  
     --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/databaseUsers/{username}/certs?pretty=true"  
  
### Response

The following example shows the JSON document returned:

    
    
    1| {  
    |  
    2|   "links" : [ {  
    3|     "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/ec13d5f09d521a5206e5d726/databaseUsers/myX509User/certs?pretty=true&pageNum=1&itemsPerPage=100",  
    4|     "rel" : "self"  
    5|   } ],  
    6|   "results" : [ {  
    7|     "_id" : 5433027191242719574,  
    8|     "createdAt" : "2019-12-03T21:00:42Z",  
    9|     "groupId" : "ec13d5f09d521a5206e5d726",  
    10|     "notAfter" : "2020-06-03T22:00:42Z",  
    11|     "subject" : "CN=myX509User"  
    12|   }, {  
    13|     "_id" : 0946028664465903704,  
    14|     "createdAt" : "2019-12-05T13:50:49Z",  
    15|     "groupId" : "ec13d5f09d521a5206e5d726",  
    16|     "notAfter" : "2020-03-05T14:50:49Z",  
    17|     "subject" : "CN=myX509User"  
    18|   } ],  
    19|   "totalCount" : 2  
    20| }  
  
What is MongoDB Atlas? →

