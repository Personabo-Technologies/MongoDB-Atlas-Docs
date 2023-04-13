Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Current LDAP Configuration

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

Gets the current LDAP over TLS configuration details for a Atlas project.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/userSecurity  
      
  
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
LDAP over TLS configuration.  
  
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
  
authzQueryTemplate

|

string

|

LDAP query template that Atlas executes to obtain the LDAP groups to which the
authenticated user belongs. This parameter applies only for user
authorization. Use the **{USER}** placeholder in the URL to substitute the
authenticated username. The query executes on a path relative to the host
specified with **hostname**. The formatting for the query must conform to RFC
4515 and RFC 4516. This parameter uses the default value of
**{USER}?memberOf?base**.  
  
caCertificate

|

string

|

Certificate Authority certificate used to verify the identify of the LDAP
server. You may use self-signed certificates.  
  
ldap

|

object

|

List of settings that configures LDAP over TLS for one Atlas project.  
  
ldap.authenticationEnabled

|

boolean

|

Flag that indicates whether this projects can use user authentication with
LDAP.  
  
ldap.authorizationEnabled

|

boolean

|

Flag that indicates whether this project has enabled user authorization with
LDAP. Enable user authentication with LDAP then enable user authorization with
LDAP.  
  
ldap.bindUsername

|

string

|

User DN that Atlas uses to connect to the LDAP server. Write in the format of
a full DN:

    
    
    | CN=BindUser,CN=Users,DC=my|ldapserver|,DC=mycompany,DC=com  
      
  
ldap.hostname

|

string

|

FQDN or IP address of the host that serves the LDAP directory. This host must
be visible to the internet or connected to your Atlas cluster with VPC
Peering.  
  
ldap.port

|

integer

|

Port on which the LDAP server listens for client connections.  
  
ldap.userToDNMapping

|

array

|

User to Distinguished Name (DN) mapping used to transform an LDAP username
into an LDAP Distinguished Name.  
  
ldap.userToDNMapping[i].match

|

string

|

Regular expression used to match against the provided LDAP username. Each
parenthesis-enclosed section represents a regular expression capture group
used by the **substitution** or **ldapQuery** template.  
  
ldap.userToDNMapping[i].substitution

|

string

|

LDAP Distinguished Name (DN) formatting template that converts the LDAP
username matched by the **match** regular expression into an LDAP
Distinguished Name.  
  
ldap.userToDNMapping[i].ldapQuery

|

string

|

LDAP query formatting template that inserts the LDAP username matched by the
**match** regular expression into an LDAP query URI as specified in RFC 4515
and RFC 4516.  
  
## Example Request

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
         --header 'Content-Type: application/json' \  
         --include \  
         --request GET "Content-Type: application/json" \  
       --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/userSecurity?pretty=true"  
  
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
    2|   "ldap" : {  
    3|     "authenticationEnabled" : true,  
    4|     "authorizationEnabled" : true,  
    5|     "authzQueryTemplate" : "{USER}?memberOf?base",  
    6|     "bindUsername" : "CN=Administrator,CN=Users,DC=atlas-ldaps-01,DC=myteam,DC=com",  
    7|     "hostname" : "atlas-ldaps-01.ldap.myteam.com",  
    8|     "port" : 636,  
    9|     "userToDNMapping" : [ {  
    10|       "match" : "(.*)",  
    11|       "substitution" : "CN={0},CN=Users,DC=atlas-ldaps-01,DC=myteam,DC=com"  
    12|     } ]  
    13|   }  
    14| }  
  
What is MongoDB Atlas? →

