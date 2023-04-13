Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create Access List Entries for One Organization API Key

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

Create one or more new access list entries for the specified API Key.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList  
      
  
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

Unique identifier for the Organization API Key for which you want to create a
new access list entry.  
  
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

Specify an array of documents, where each document represents one access list
entry you want to add to the project. You must specify an array even if you
are only associating a single access list entry to the project.

When you submit a `POST` request containing **ipAddress** or **cidrBlock**
values which are not already present in the access list, Atlas adds those
entries to the list of existing entries in the access list. Atlas does not set
the access list to only contain the entries specified in the request.

## Note

Atlas supports up to 500 API keys within a single organization.

In the following table, `[i]` represents an array index.

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
[i].ipAddress

|

string

|

Required

|

IP address to be added to the access list for the API key. Set this parameter
or **cidrBlock** , not both.  
  
[i].cidrBlock

|

string

|

Required

|

CIDR-notation block of IP addresses to be added to the access list for the API
key. Set this parameter or **ipAddress** , not both.  
  
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

Each object within the `results` array is one access list entry.

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
    2|      --header 'Accept: application/json' \  
    3|      --header 'Content-Type: application/json' \  
    4|      --include \  
    5|      --request POST "https://cloud.mongodb.com/api/public/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList?pretty=true" \  
    6|      --data '  
    7|        [{  
    8|           "ipAddress" : "77.54.32.11"  
    9|        }]'  
  
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
    3|     "href" : "https://cloud.mongodb.com/api/public/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList?pretty=true&pageNum=1&itemsPerPage=100",  
    4|     "rel" : "self"  
    5|   } ],  
    6|   "results" : [ {  
    7|     "cidrBlock" : "206.252.195.126/32",  
    8|     "count" : 47,  
    9|     "created" : "2019-01-24T16:26:37Z",  
    10|     "ipAddress" : "206.252.195.126",  
    11|     "lastUsed" : "2019-01-25T16:32:47Z",  
    12|     "lastUsedAddress" : "206.252.195.126",  
    13|     "links" : [ {  
    14|       "href" : "https://cloud.mongodb.com/api/public/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/206.252.195.126",  
    15|       "rel" : "self"  
    16|     } ]  
    17|   }, {  
    18|     "cidrBlock" : "76.54.32.11/32",  
    19|     "count" : 0,  
    20|     "created" : "2019-01-24T21:09:05Z",  
    21|     "ipAddress" : "76.54.32.11",  
    22|     "links" : [ {  
    23|       "href" : "https://cloud.mongodb.com/api/public/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/76.54.32.11",  
    24|       "rel" : "self"  
    25|     } ]  
    26|   }, {  
    27|     "cidrBlock" : "77.54.32.11/32",  
    28|     "count" : 0,  
    29|     "created" : "2019-01-25T16:32:47Z",  
    30|     "ipAddress" : "77.54.32.11",  
    31|     "links" : [ {  
    32|       "href" : "https://cloud.mongodb.com/api/public/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/77.54.32.11",  
    33|       "rel" : "self"  
    34|     } ]  
    35|   } ],  
    36|   "totalCount" : 3  
    37| }  
  
What is MongoDB Atlas? →

