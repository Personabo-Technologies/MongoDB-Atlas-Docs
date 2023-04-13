Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Status of a Request to Verify LDAP Configuration

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Returns the status of the most recent request for verification of an LDAP over
TLS configuration. Atlas returns an HTTP 404 error if you request the status
of any request other than the most recent.

## Note

  * Explaining RFC 4515 and RFC 4516 falls out of scope of the Atlas documentation. Review these RFCs or refer to your preferred LDAP documentation.

  * Groups and projects are synonymous. `{GROUP-ID}` and `{GROUP-ID}` have the same meaning. The unique identifier for your existing projects/groups remains the same. This endpoint and corresponding endpoints use the terms `groups` and `groupId`.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/userSecurity/ldap/verify/{REQUEST-ID}  
      
  
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

Unique 24-hexadecimal digit string for the Atlas project associated with the
verification request.  
  
REQUEST-ID

|

string

|

Required

|

Unique 24-hexadecimal digit string for request to verify an LDAP
configuration. Returned in the response document to the Verify |ldap|
Configuration endpoint.  
  
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

## Response Elements

Name

|

Type

|

Description  
  
||  
  
groupId

|

string

|

Unique 24-hexadecimal digit string that represents the Atlas project
associated with the request to verify an LDAP over TLS configuration.  
  
links

|

object array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
request

|

object

|

Contains the details of the request to verify an LDAP over TLS configuration.
Atlas doesn't return the **bindPassword** in the response.  
  
request.bindUsername

|

string

|

User DN that Atlas uses to connect to the LDAP server.  
  
request.hostname

|

string

|

FQDN or IP address of the host that serves the LDAP directory. This host must
be visible to the internet or connected to your Atlas cluster with VPC
Peering.  
  
request.port

|

integer

|

Port on which the LDAP server listens for client connections from Atlas.  
  
requestId

|

string

|

Unique 24-hexadecimal digit string that represents the request to verify the
LDAP over TLS configuration.  
  
status

|

string

|

Current phase of the LDAP over TLS configuration workflow returned at the time
of the request. Atlas returns one of the following values: **PENDING** ,
**SUCCESS** , and **FAIL**.  
  
validations

|

array

|

List of validation messages related to the verification of the provided LDAP
over TLS configuration details. The array contains a document for each test
that Atlas runs. Atlas stops running tests after the first failure. Atlas
returns one of the following values:

 **{**

 **status: "OK" || "FAIL",**

 **validationType: "SERVER_SPECIFIED"**

 **}**

 **{**

 **status: "OK" || "FAIL",**

 **validationType: "CONNECT"**

 **}**

 **{**

 **status: "OK" || "FAIL",**

 **validationType: "AUTHENTICATE"**

 **}**

 **{**

 **status: "OK" || "FAIL",**

 **validationType: "AUTHORIZATION_ENABLED"**

 **}**

 **{**

 **status: "OK" || "FAIL",**

 **validationType: "PARSE_AUTHZ_QUERY_TEMPLATE"**

 **}**

 **{**

 **status: "OK" || "FAIL",**

 **validationType: "QUERY_SERVER"**

 **}**  
  
## Example Request

The following example requests the status of a request to verify an LDAP
configuration.

    
    
    curl --include --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --digest \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/userSecurity/ldap/verify/{REQUEST-ID}?pretty=true"  
  
## Example Response

The following example returns a status of `SUCCESS`.

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
    2|   "groupId" : "{GROUP-ID}",  
    3|   "links" : [ {  
    4|      "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/userSecurity/ldap/verify/{REQUEST-ID}",  
    5|      "rel" : "self"  
    6|   } ],  
    7|   "request" : {  
    8|   "bindUsername" : "CN=Administrator,CN=Users,DC=atlas-ldaps-01,DC=myteam,DC=com",  
    9|   "hostname" : "atlas-ldaps-01.ldap.myteam.com",  
    10|   "port" : 636  
    11|   },  
    12|   "requestId" : "{REQUEST-ID}",  
    13|   "status" : "SUCCESS",  
    14|   "validations" : [ {  
    15|     "status" : "OK",  
    16|     "validationType" : "SERVER_SPECIFIED"  
    17|   }, {  
    18|     "status" : "OK",  
    19|     "validationType" : "CONNECT"  
    20|   }, {  
    21|     "status" : "OK",  
    22|     "validationType" : "AUTHENTICATE"  
    23|   }, {  
    24|     "status" : "OK",  
    25|     "validationType" : "AUTHORIZATION_ENABLED"  
    26|   }, {  
    27|     "status" : "OK",  
    28|     "validationType" : "PARSE_AUTHZ_QUERY_TEMPLATE"  
    29|   }, {  
    30|     "status" : "OK",  
    31|     "validationType" : "QUERY_SERVER"  
    32|   } ]  
    33| }  
  
What is MongoDB Atlas? →

