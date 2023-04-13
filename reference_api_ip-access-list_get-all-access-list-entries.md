Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Project IP Access List

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
  * Example Header
  * Example Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Access List Replaces Whitelist

This resource replaces the whitelist resource. Atlas removed whitelists in
July 2021. Update your applications to use this new resource.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Important

The `/groups/{GROUP-ID}/accessList` endpoint manages the database IP access
list. This endpoint is distinct from the orgs/{ORG-ID}/apiKeys/{API-KEY-
ID}/accesslist endpoint, which manages the access list for Atlas
organizations.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Syntax

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/accessList  
      
  
### Request Path Parameters

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
GROUP-ID

|

string

|

Required

|

Unique identifier for the project from which you want to retrieve access list
entries.  
  
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

Each element in the **result** array is one access list entry associated to
the project IP access list.

Name

|

Type

|

Description  
  
||  
  
awsSecurityGroup

|

string

|

Unique identifier of AWS security group in this access list entry.  
  
cidrBlock

|

string

|

Range of IP addresses in CIDR notation in this access list entry.  
  
comment

|

string

|

Comment associated with this access list entry.  
  
deleteAfterDate

|

date

|

Timestamp in ISO 8601 date and time format in UTC after which Atlas deletes
the temporary access list entry. Atlas returns this field if you specified an
expiration date when creating this access list entry.  
  
groupId

|

string

|

Unique identifier of the project to which this access list entry applies.  
  
ipAddress

|

string

|

Entry using an IP address in this access list entry.  
  
links

|

object array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/accessList?pretty=true"  
  
## Example Response

### Example Header

    
    
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
  
### Example Body

    
    
    1| {  
    |  
    2|   "links": [],  
    3|   "results": [  
    4|     {  
    5|       "cidrBlock": "192.0.2.0/24",  
    6|       "comment": "IP address for Application Server A",  
    7|       "groupId": "{GROUP-ID}",  
    8|       "ipAddress": "192.0.2.15",  
    9|       "links": []  
    10|     },  
    11|     {  
    12|       "cidrBlock": "203.0.113.0/24",  
    13|       "comment": "CIDR block for Application Server B - D",  
    14|       "groupId": "{GROUP-ID}",  
    15|       "links": []  
    16|     },  
    17|     {  
    18|       "awsSecurityGroup": "sg-0026348ec11780bd1",  
    19|       "comment": "Access Listed AWS Security Group",  
    20|       "groupId": "{GROUP-ID}",  
    21|       "links": []        ]  
    22|   ],  
    23|   "totalCount": 3  
    24| }  
  
What is MongoDB Atlas? →

