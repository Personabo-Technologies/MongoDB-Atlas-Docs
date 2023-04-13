Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return All Snapshots Of One Serverless Instance

Share Feedback

On this page

  * Required Roles
  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Return all snapshots of one serverless instance from the specified project.

## Required Roles

Your API Key must have the `Project Read Only` role to successfully call this
resource.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{groupId}/serverless/{instanceName}/backup/snapshots  
      
  
### Request Path Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
groupId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies your project.  
  
instanceName

|

string

|

Required

|

Human-readable label that identifies your serverless instance.  
  
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

This endpoint doesn't use HTTP request body parameters.

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

Each element in the **result** array is one serverless instance.

Name

|

Type

|

Description  
  
||  
  
createdAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas took the
snapshot. Atlas sorts the **results** document in descending order based on
this date.  
  
expiresAt

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas deletes the
snapshot.  
  
id

|

string

|

Unique 24-hexadecimal digit string that identifies your snapshot.  
  
mongodVersion

|

string

|

Version of the MongoDB server.  
  
serverlessInstanceName

|

string

|

Human-readable label given to the serverless instance from which Atlas took
this snapshot.  
  
snapshotType

|

string

|

Type of snapshot. Atlas returns **scheduled**.  
  
status

|

string

|

Current status of the snapshot. Atlas can return one of the following values:

  *  **queued**

  *  **inProgress**

  *  **completed**

  *  **failed**

  
  
storageSizeBytes

|

integer

|

Size of the snapshot in bytes.  
  
## Example Request

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
         --header 'Content-Type: application/json' \  
         --include \  
         --request GET 'https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName}/backup/snapshots?pretty=true'  
  
## Example Response

### Response Header

    
    
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
  
### Response Body

    
    
    1| {  
    |  
    2|   "links": [  
    3|     {  
    4|         "rel": "self",  
    5|         "href": "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName}/backup/snapshots?pageNum=1&itemsPerPage=100"  
    6|     }  
    7|   ],  
    8|   "totalCount": 1,  
    9|   "results": [  
    10|     {  
    11|       "createdAt": "2020-12-20T00:00:00Z",  
    12|       "expiresAt": "2021-02-19T21:04:52Z",  
    13|       "id": "{snapshotId}",  
    14|       "mongodVersion": "5.0.0",  
    15|       "serverlessInstanceName": "{instanceName}",  
    16|       "snapshotType": "scheduled",  
    17|       "status": "completed"  
    18|       "storageSizeBytes": 1024,  
    19|     }  
    20|   ]  
    21| }  
  
What is MongoDB Atlas? →

