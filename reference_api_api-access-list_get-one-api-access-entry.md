Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Access List Entry for One Organization API Key

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Retrieve information on a single API Key access list entry using the unique
identifier for the API Key and desired permitted address.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/{ACCESS-LIST-ENTRY}  
      
  
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
  
ACCESS-LIST-ENTRY

|

string

|

Required

|

IP address or CIDR block. If the entry includes a subnet mask, such as
`192.0.2.0/24`, use the URL-encoded value `%2F` for the forward slash `/`.  
  
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

This endpoint doesn't use HTTP request body parameters.

## Response

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

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/192.0.2.0%2F24?pretty=true"  
  
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
    2|   "cidrBlock": "192.0.2.0/24",  
    3|   "count": 0,  
    4|   "created": "{ISO-TIMESTAMP}",  
    5|   "links": [  
    6|     {  
    7|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accessList/192.0.2.0%2F24",  
    8|       "rel": "self"  
    9|     },  
    10|     {  
    11|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}",  
    12|       "rel": "http://mms.mongodb.com/apiKeys"  
    13|     }  
    14|   ]  
    15| }  
  
What is MongoDB Atlas? →

