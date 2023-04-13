Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Access List Entries for One Organization API Key

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
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Retrieve information on all access list entries for the specified API Key.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList  
      
  
### Request Path Parameters

Name

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

Unique identifier for the organization to which the target API Key belongs.
Use the /orgs endpoint to retrieve all organizations to which the
authenticated user has access.  
  
API-KEY-ID

|

string

|

Required

|

Unique identifier for the API Key for which you want to retrieve access list
entries. Use the /orgs/{ORG-ID}/apiKeys endpoint to retrieve all API Keys for
the specified organization to which the authenticated user has access.  
  
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

Each **result** is one access list entry.

Name

|

Type

|

Description  
  
||  
  
cidrBlock

|

string

|

CIDR-notated range of permitted IP addresses.  
  
count

|

integer

|

Total number of requests that have originated from this IP address.  
  
created

|

string

|

Timestamp in ISO 8601 date and time format in UTC when this IP address was
added to the API access list.  
  
ipAddress

|

string

|

IP address in the API access list.  
  
lastUsed

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the most recent request
that originated from this IP address. This parameter only appears if at least
one request has originated from this IP address, and is only updated when a
permitted resource is accessed.  
  
lastUsedAddress

|

string

|

IP address from which the last call to the API was issued. This parameter only
appears if at least one request has originated from this IP address.  
  
links

|

array of objects

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList?pretty=true"  
  
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
    2|   "links" : [ {  
    3|   "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/599c510c80eef518f3b63fe1/apiKeys/5c49e72980eef544a218f8f8/accessList/?pretty=true&pageNum=1&itemsPerPage=100",  
    4|   "rel" : "self"  
    5|   } ],  
    6|   "results" : [ {  
    7|     "cidrBlock" : "147.58.184.16/32",  
    8|     "count" : 0,  
    9|     "created" : "2019-01-24T16:34:57Z",  
    10|     "ipAddress" : "147.58.184.16",  
    11|     "lastUsed" : "2019-01-24T20:18:25Z",  
    12|     "lastUsedAddress": "147.58.184.16",  
    13|     "links" : [ {  
    14|       "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/147.58.184.16",  
    15|       "rel" : "self"  
    16|     } ]  
    17|   }, {  
    18|     "cidrBlock" : "84.255.48.125/32",  
    19|     "count" : 0,  
    20|     "created" : "2019-01-24T16:26:37Z",  
    21|     "ipAddress" : "84.255.48.125",  
    22|     "lastUsed" : "2019-01-24T20:18:25Z",  
    23|     "lastUsedAddress": "84.255.48.125",  
    24|     "links" : [ {  
    25|       "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/206.252.195.126",  
    26|       "rel" : "self"  
    27|     } ]  
    28|   } ],  
    29|   "totalCount" : 2  
    30| }  
  
What is MongoDB Atlas? →

