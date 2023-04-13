Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Verify One LDAP Configuration

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

Requests a verification of an LDAP configuration over TLS for an Atlas
project. Pass the `requestId` in the response object to the Verify |ldap|
Configuration endpoint to get the status of a verification request. Atlas
retains only the most recent request for each project.

## Note

  * Explaining RFC 4515 and RFC 4516 falls out of scope of the Atlas documentation. Review these RFCs or refer to your preferred LDAP documentation.

  * Groups and projects are synonymous. `{GROUP-ID}` and `{GROUP-ID}` have the same meaning. The unique identifier for your existing projects/groups remains the same. This endpoint and corresponding endpoints use the terms `groups` and `groupId`.

  * This endpoint does not verify the `ldap.userToDNMapping` document array. To verify that users can authenticate with this parameter, use the mongoldap package component bundled with MongoDB Enterprise 4.0 or later with a config file that includes the same LDAP parameters that you specify for Atlas.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/userSecurity/ldap/verify  
      
  
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

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
authzQueryTemplate

|

string

|

Optional

|

LDAP query template that Atlas executes to obtain the LDAP groups to which the
authenticated user belongs. This parameter applies only for user
authorization. Use the **{USER}** placeholder in the URL to substitute the
authenticated username. The query executes on a path relative to the host
specified with **hostname**. The formatting for the query must conform to RFC
4515 and RFC 4516. This parameter uses the default value of
**{USER}?memberOf?base**.  
  
bindUsername

|

string

|

Required

|

User DN that Atlas uses to connect to the LDAP server. Write in the format of
a full DN:

    
    
    | CN=BindUser,CN=Users,DC=my|ldapserver|,DC=mycompany,DC=com  
      
  
bindPassword

|

string

|

Required

|

Password used to authenticate the **bindUsername**.  
  
caCertificate

|

string

|

Optional

|

Certificate Authority certificate used to verify the identify of the LDAP
server. You may use self-signed certificates.  
  
hostname

|

string

|

Required

|

FQDN or IP address of the host that serves the LDAP directory. This host must
be visible to the internet or connected to your Atlas cluster with VPC
Peering.  
  
port

|

integer

|

Required

|

Port to which the LDAP server listens for client connections. This parameter
use a default value of **636**.  
  
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

## Important

### Use UNIX Line Breaks for Certificate Authority File

This API resource only accepts UNIX line breaks (`\n`) in the
**caCertificate** field.

    
    
    1| curl --include --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --digest \  
    5|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/userSecurity/ldap/verify?pretty=true" \  
    6|      --data '  
    7|        {  
    8|          "authzQueryTemplate": "{USER}?memberOfGroup?base",  
    9|          "bindUsername":"N=Administrator,CN=Users,DC=atlas-ldaps-01,DC=myteam,DC=com",  
    10|          "bindPassword":"MyldapPassWord",  
    11|          "caCertificate" : "--BEGIN CERTIFICATE--\nMIICyDCCAbCgAwIBAgIUTZjoFW/ohMYNo5G61XxunFGC+y8wDQYJKoZIhvcNAQEL\nBQAwEjEQMA4GA1UEAwwHVGVzdCBDQTAeFw0yMTA5MDMyMjE1NThaFw0zMTA5MDEy\nMjE1NThaMBIxEDAOBgNVBAMMB1Rlc3QgQ0EwggEiMA0GCSqGSIb3DQEBAQUAA4IB\nDwAwggEKAoIBAQCg7VJRBbhm6HHZh3gYy8y320OVkV7GRwO7K82ucJbgaaa5GY+x\npiNg0zIXlNUBLclMm7jToyGjzDBd1Aw+Snys2DTrkvAFvvk/peJQL9HA4QdicS6x\nD6eQjw6/LA3hct1xaHo8Uf+OSS+hg/tb4MZRoKUCnxAWRr+DNpSwv3ln0sDv0Mrh\n+V7G/Xly64syCuWRVA1qycWm6koZo0uA/ZLwdL825aCve3ArKzcSw1UwR3Cav52q\n8K1GDcRxgq/6A9T+6k9mw2sIm6ESMMhwn75n6bBH16XKELQKbCO7DCSh9bqXezvK\n1KN32aEnxgfszXjaM5DZwoDrGNBq+bWjokfHAgMBAAGjFjAUMBIGA1UdEwEB/wQI\nMAYBAf8CAQAwDQYJKoZIhvcNAQELBQADggEBAGPRgtRijtvsfbWZ2NaZ6xuAdNBt\nyIbK8crl01DO7ukCvHZ6R528hq33gvL+8x7uhlimA3gMw3swtD4GdEcnQ5vgKIU2\nt+ghjlzdKHhJWiSzoLqTFQvAKwTpM2RKRUQ0FWmZqlLyrxCVu54gpPDKillszpeU\noaHSAZnu+k3V8SYf0J3EOAizdSqo0RwltLExNmT8hlUBdQuI303ljxIdZbTzECBo\nfNAdcEEOdOExt6VyrnJFT0P5kQmE+IL1mSkbbEVgifOiux4HRT4FuFBavBg39G7G\n/QRxQEzTaMbmOeK3o9Vm+/IgBa9rtiPZPqSArq9jED+CY9bmrwzIDsA2ujA=\n--END CERTIFICATE--",  
    12|          "hostname":"atlas-ldaps-01.ldap.myteam.com",  
    13|          "port": 636  
    14|        }'  
  
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
    2|   "groupId" : "{GROUP-ID}",  
    3|   "links" : [ {  
    4|      "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/userSecurity/ldap/verify/{REQUEST-ID}",  
    5|      "rel" : "self"  
    6|   } ],  
    7|   "request" : {  
    8|     "bindUsername" : "CN=Administrator,CN=Users,DC=atlas-ldaps-01,DC=myteam,DC=com",  
    9|     "caCertificate" : "--BEGIN CERTIFICATE--\nMIICyDCCAbCgAwIBAgIUTZjoFW/ohMYNo5G61XxunFGC+y8wDQYJKoZIhvcNAQEL\nBQAwEjEQMA4GA1UEAwwHVGVzdCBDQTAeFw0yMTA5MDMyMjE1NThaFw0zMTA5MDEy\nMjE1NThaMBIxEDAOBgNVBAMMB1Rlc3QgQ0EwggEiMA0GCSqGSIb3DQEBAQUAA4IB\nDwAwggEKAoIBAQCg7VJRBbhm6HHZh3gYy8y320OVkV7GRwO7K82ucJbgaaa5GY+x\npiNg0zIXlNUBLclMm7jToyGjzDBd1Aw+Snys2DTrkvAFvvk/peJQL9HA4QdicS6x\nD6eQjw6/LA3hct1xaHo8Uf+OSS+hg/tb4MZRoKUCnxAWRr+DNpSwv3ln0sDv0Mrh\n+V7G/Xly64syCuWRVA1qycWm6koZo0uA/ZLwdL825aCve3ArKzcSw1UwR3Cav52q\n8K1GDcRxgq/6A9T+6k9mw2sIm6ESMMhwn75n6bBH16XKELQKbCO7DCSh9bqXezvK\n1KN32aEnxgfszXjaM5DZwoDrGNBq+bWjokfHAgMBAAGjFjAUMBIGA1UdEwEB/wQI\nMAYBAf8CAQAwDQYJKoZIhvcNAQELBQADggEBAGPRgtRijtvsfbWZ2NaZ6xuAdNBt\nyIbK8crl01DO7ukCvHZ6R528hq33gvL+8x7uhlimA3gMw3swtD4GdEcnQ5vgKIU2\nt+ghjlzdKHhJWiSzoLqTFQvAKwTpM2RKRUQ0FWmZqlLyrxCVu54gpPDKillszpeU\noaHSAZnu+k3V8SYf0J3EOAizdSqo0RwltLExNmT8hlUBdQuI303ljxIdZbTzECBo\nfNAdcEEOdOExt6VyrnJFT0P5kQmE+IL1mSkbbEVgifOiux4HRT4FuFBavBg39G7G\n/QRxQEzTaMbmOeK3o9Vm+/IgBa9rtiPZPqSArq9jED+CY9bmrwzIDsA2ujA=\n--END CERTIFICATE--",  
    10|     "hostname" : "atlas-ldaps-01.ldap.myteam.com",  
    11|     "port" : 636  
    12|   },  
    13|   "requestId" : "{REQUEST-ID}",  
    14|   "status" : "PENDING",  
    15|   "validations" : [ ],  
    16| }  
  
What is MongoDB Atlas? →

