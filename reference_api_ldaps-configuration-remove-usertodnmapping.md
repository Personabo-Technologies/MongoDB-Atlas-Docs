Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete One LDAP userToDNMapping

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

Removes the current **userToDNMapping** from the LDAP configuration for an
Atlas project. A **userToDNMapping** maps the username provided to a `mongod`
or `mongos` process for authentication to an LDAP Distinguished Name (DN).

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    DELETE /groups/{GROUP-ID}/userSecurity  
      
  
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
  
ldap.authzQueryTemplate

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
  
## Example Request

The following example unsets the values for **caCertificate** and
**authzQueryTemplate** from the current LDAP configuration:

    
    
    1| curl --include --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --digest \  
    4|      --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/userSecurity/ldap/userToDNMapping?pretty=true" \  
    5|      --data '  
  
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
    8|     "port" : 636  
    9|   }  
    10| }  
  
What is MongoDB Atlas? →

