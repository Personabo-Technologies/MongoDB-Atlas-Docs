Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Save One LDAP Configuration

Share Feedback

On this page

  * Syntax
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

Saves an LDAP configuration for an Atlas project. This endpoint doesn't verify
connectivity using the provided LDAP over TLS configuration details. To verify
a configuration before saving it, use the Verify |ldap| Configuration
endpoint.

## Note

  * Explaining RFC 4515 and RFC 4516 falls out of scope of the Atlas documentation. Review these RFCs or refer to your preferred LDAP documentation.

  * Groups and projects are synonymous. `{GROUP-ID}` and `{GROUP-ID}` have the same meaning. The unique identifier for your existing projects/groups remains the same. This endpoint and corresponding endpoints use the terms `groups` and `groupId`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    PATCH /groups/{GROUP-ID}/userSecurity  
      
  
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

## Tip

Pass an empty string to delete a previously assigned value:

    
    
    | "authzQueryTemplate": ""  
      
  
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

## Tip

Pass an empty string to delete a previously assigned value:

    
    
    | "caCertificate": ""  
      
  
ldap

|

object

|

Required

|

List of settings that configures LDAP over TLS for one Atlas project.  
  
ldap.authenticationEnabled

|

boolean

|

Required

|

Specifies whether user authentication with LDAP is enabled.  
  
ldap.authorizationEnabled

|

boolean

|

Optional

|

Specifies whether user authorization with LDAP is enabled. You cannot enable
user authorization with LDAP without first enabling user authentication with
LDAP.  
  
ldap.bindUsername

|

string

|

Required

|

User DN that Atlas uses to connect to the LDAP server. Write in the format of
a full DN:

    
    
    | CN=BindUser,CN=Users,DC=my|ldapserver|,DC=mycompany,DC=com  
      
  
ldap.hostname

|

string

|

Required

|

FQDN or IP address of the host that serves the LDAP directory. This host must
be visible to the internet or connected to your Atlas cluster with VPC
Peering.  
  
ldap.port

|

integer

|

Required

|

Port to which the LDAP server listens for client connections. This parameter
use a default value of **636**.  
  
ldap.userToDNMapping

|

array

|

Required

|

Maps an LDAP username for authentication to an LDAP Distinguished Name (DN).
Each document contains a **match** regular expression and either a
**substitution** or **ldapQuery** template used to transform the LDAP username
extracted from the regular expression. Atlas steps through the each document
in the array in the given order, checking the authentication username against
the **match** filter. If a match is found, Atlas applies the transformation
and uses the output to authenticate the user. Atlas does not check the
remaining documents in the array. To learn more, see
`security.ldap.userToDNMapping`.

The following example provides a **match** regular expression that matches all
users and substitutes the username into the **{0}** argument of the
**substitution** template to create an LDAP DN.

    
    
    | "userToDNMapping": [  
      
      {  
       "match":"(.*)",  
       "substitution":"CN={0},CN=Users,DC=my-atlas-ldap-server,DC=myteam,DC=com"  
      }  
    ]  
  
ldap.userToDNMapping[i].match

|

string

|

Required

|

Regular expression to match against a provided LDAP username. Each
parenthesis-enclosed section represents a regular expression capture group
that the **substitution** or **ldapQuery** template can use.  
  
ldap.userToDNMapping[i].substitution

|

string

|

Required

|

LDAP Distinguished Name (DN) formatting template that converts the LDAP name
matched by the **match** regular expression into an LDAP Distinguished Name.
Atlas replaces each numeric value with the corresponding regular expression
capture group extracted from the LDAP username that matched the **match**
regular expression.

## Example

    
    
    | "substitution":"CN={0},CN=Users,DC=my-atlas-ldap-server,DC=myteam,DC=com"``  
      
  
Each document in the **ldap.userToDNMapping.match** array must contain either
a **substitution** or **ldapQuery** field, but not both.  
  
ldap.userToDNMapping[i].ldapQuery

|

string

|

Required

|

LDAP query formatting template that inserts the LDAP name matched by the
**match** regular expression into an LDAP query URI. The formatting for the
query must conform to RFC 4515 and RFC 4516. Atlas replaces each numeric value
with the corresponding regular expression capture group extracted from the
LDAP username that matched the **match** regular expression.

## Example

    
    
    | "ou=engineering,dc=example, dc=com??one?(user={0})"  
      
  
Each document in the **ldap.userToDNMapping.match** array must contain either
a **substitution** or **ldapQuery** field, but not both.  
  
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

## Important

### Use UNIX Line Breaks for Certificate Authority File

This API resource only accepts UNIX line breaks (`\n`) in the
**caCertificate** field.

    
    
    1| curl --include --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --digest \  
    5|      --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/userSecurity?pretty=true" \  
    6|      --data '  
    7|        {  
    8|          "ldap": {  
    9|            "authenticationEnabled":true,  
    10|            "authorizationEnabled":true,  
    11|            "authzQueryTemplate":"{USER}?memberOf?base",  
    12|            "bindUsername": "CN=Administrator,CN=Users,DC=atlas-ldaps-01,DC=myteam,DC=com",  
    13|            "bindPassword":"MyldapPassWord",  
    14|            "caCertificate" : "--BEGIN CERTIFICATE--\nMIICyDCCAbCgAwIBAgIUTZjoFW/ohMYNo5G61XxunFGC+y8wDQYJKoZIhvcNAQEL\nBQAwEjEQMA4GA1UEAwwHVGVzdCBDQTAeFw0yMTA5MDMyMjE1NThaFw0zMTA5MDEy\nMjE1NThaMBIxEDAOBgNVBAMMB1Rlc3QgQ0EwggEiMA0GCSqGSIb3DQEBAQUAA4IB\nDwAwggEKAoIBAQCg7VJRBbhm6HHZh3gYy8y320OVkV7GRwO7K82ucJbgaaa5GY+x\npiNg0zIXlNUBLclMm7jToyGjzDBd1Aw+Snys2DTrkvAFvvk/peJQL9HA4QdicS6x\nD6eQjw6/LA3hct1xaHo8Uf+OSS+hg/tb4MZRoKUCnxAWRr+DNpSwv3ln0sDv0Mrh\n+V7G/Xly64syCuWRVA1qycWm6koZo0uA/ZLwdL825aCve3ArKzcSw1UwR3Cav52q\n8K1GDcRxgq/6A9T+6k9mw2sIm6ESMMhwn75n6bBH16XKELQKbCO7DCSh9bqXezvK\n1KN32aEnxgfszXjaM5DZwoDrGNBq+bWjokfHAgMBAAGjFjAUMBIGA1UdEwEB/wQI\nMAYBAf8CAQAwDQYJKoZIhvcNAQELBQADggEBAGPRgtRijtvsfbWZ2NaZ6xuAdNBt\nyIbK8crl01DO7ukCvHZ6R528hq33gvL+8x7uhlimA3gMw3swtD4GdEcnQ5vgKIU2\nt+ghjlzdKHhJWiSzoLqTFQvAKwTpM2RKRUQ0FWmZqlLyrxCVu54gpPDKillszpeU\noaHSAZnu+k3V8SYf0J3EOAizdSqo0RwltLExNmT8hlUBdQuI303ljxIdZbTzECBo\nfNAdcEEOdOExt6VyrnJFT0P5kQmE+IL1mSkbbEVgifOiux4HRT4FuFBavBg39G7G\n/QRxQEzTaMbmOeK3o9Vm+/IgBa9rtiPZPqSArq9jED+CY9bmrwzIDsA2ujA=\n--END CERTIFICATE--",  
    15|            "hostname":"atlas-ldaps-01.ldap.myteam.com",  
    16|            "port":636,  
    17|            "userToDNMapping" : [ {  
    18|              "match" : "(.*)",  
    19|              "substitution" : "CN={0},CN=Users,DC=atlas-ldaps-01,DC=myteam,DC=com"  
    20|            } ]  
    21|          }  
    22|        }'  
  
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
    7|     "caCertificate" : "--BEGIN CERTIFICATE--\nMIICyDCCAbCgAwIBAgIUTZjoFW/ohMYNo5G61XxunFGC+y8wDQYJKoZIhvcNAQEL\nBQAwEjEQMA4GA1UEAwwHVGVzdCBDQTAeFw0yMTA5MDMyMjE1NThaFw0zMTA5MDEy\nMjE1NThaMBIxEDAOBgNVBAMMB1Rlc3QgQ0EwggEiMA0GCSqGSIb3DQEBAQUAA4IB\nDwAwggEKAoIBAQCg7VJRBbhm6HHZh3gYy8y320OVkV7GRwO7K82ucJbgaaa5GY+x\npiNg0zIXlNUBLclMm7jToyGjzDBd1Aw+Snys2DTrkvAFvvk/peJQL9HA4QdicS6x\nD6eQjw6/LA3hct1xaHo8Uf+OSS+hg/tb4MZRoKUCnxAWRr+DNpSwv3ln0sDv0Mrh\n+V7G/Xly64syCuWRVA1qycWm6koZo0uA/ZLwdL825aCve3ArKzcSw1UwR3Cav52q\n8K1GDcRxgq/6A9T+6k9mw2sIm6ESMMhwn75n6bBH16XKELQKbCO7DCSh9bqXezvK\n1KN32aEnxgfszXjaM5DZwoDrGNBq+bWjokfHAgMBAAGjFjAUMBIGA1UdEwEB/wQI\nMAYBAf8CAQAwDQYJKoZIhvcNAQELBQADggEBAGPRgtRijtvsfbWZ2NaZ6xuAdNBt\nyIbK8crl01DO7ukCvHZ6R528hq33gvL+8x7uhlimA3gMw3swtD4GdEcnQ5vgKIU2\nt+ghjlzdKHhJWiSzoLqTFQvAKwTpM2RKRUQ0FWmZqlLyrxCVu54gpPDKillszpeU\noaHSAZnu+k3V8SYf0J3EOAizdSqo0RwltLExNmT8hlUBdQuI303ljxIdZbTzECBo\nfNAdcEEOdOExt6VyrnJFT0P5kQmE+IL1mSkbbEVgifOiux4HRT4FuFBavBg39G7G\n/QRxQEzTaMbmOeK3o9Vm+/IgBa9rtiPZPqSArq9jED+CY9bmrwzIDsA2ujA=\n--END CERTIFICATE--",  
    8|     "hostname" : "atlas-ldaps-01.ldap.myteam.com",  
    9|     "port" : 636,  
    10|     "userToDNMapping" : [ {  
    11|       "match" : "(.*)",  
    12|       "substitution" : "CN={0},CN=Users,DC=atlas-ldaps-01,DC=myteam,DC=com"  
    13|     } ]  
    14|   }  
    15| }  
  
What is MongoDB Atlas? →

