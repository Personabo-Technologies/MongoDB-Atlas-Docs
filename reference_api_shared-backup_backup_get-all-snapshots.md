Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Snapshots for an M2/M5 Cluster

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

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Retrieve all snapshots for a specified `M2` or `M5` shared cluster.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/tenant/snapshots  
      
  
### Request Path Parameters

Path Element

|

Description  
  
|  
  
`GROUP-ID`

|

Unique identifier of the project for the Atlas cluster.  
  
`CLUSTER-NAME`

|

Name of the Atlas cluster for which you want to retrieve snapshots.  
  
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

Name

|

Type

|

Description  
  
||  
  
`finishTime`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when Atlas marked the
snapshot as `COMPLETED`.  
  
`id`

|

objectId

|

Unique identifier of the snapshot.  
  
`mongoDBVersion`

|

string

|

Version of the MongoDB server.  
  
`scheduledTime`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when the snapshot is
scheduled to be taken.  
  
`startTime`

|

date

|

Timestamp in ISO 8601 date and time format in UTC when Atlas began taking the
snapshot.  
  
`status`

|

string

|

Current status of the snapshot. Possible values are:

  * `COMPLETED`

  * `FAILED`

  * `PENDING`

  * `QUEUED`

  * `RUNNING`

  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b69d0349b15c62cdfc38b78/clusters/M2AWS/backup/tenant/snapshots  
  
## Example Response

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
      
    
    {  
      
      "results" : [ {  
        "finishTime" : "2019-04-26T14:08:07Z",  
        "id" : "5cc310ace5dc7ce369814bc8",  
        "mongoDBVersion" : "4.2.7",  
        "scheduledTime" : "2019-04-26T12:00:00Z",  
        "startTime" : "2019-04-26T14:07:53Z",  
        "status" : "FAILED"  
      } ],  
      "totalCount" : 1  
    }  
  
What is MongoDB Atlas? →

