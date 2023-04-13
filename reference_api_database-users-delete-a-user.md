Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete a Database User

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

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API uses HTTP Digest Authentication. Provide your
Atlas username as the username and Atlas Administration API key as the
password as part of the HTTP request.

This endpoint requires that the Atlas user has the `Owner` role. To view the
available Atlas users, click on Users & Teams in the left-hand navigation.

For complete documentation on configuring API access for an Atlas project, see
Get Started with the Atlas Administration API.

The parameters that this resource requires depend upon the authentication
mechanism the database uses. Select from one of the following authentication
mechanisms:

SCRAM-SHA

X.509

LDAP

AWS IAM

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    DELETE /groups/{GROUP-ID}/databaseUsers/{databaseName}/{USERNAME}  
      
  
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

Unique 24-hexadecimal string that identifies the project.  
  
DATABASE-NAME

|

string

|

Required

|

Database against which the database user authenticates. Database users must
provide both a username and authentication database to log into MongoDB.

You may set this parameter value as:

SCRAM-SHA

X.509

LDAP

AWS IAM

 **admin** if the database user authenticates with SCRAM-SHA.

If you don't set an authentication mechanism, Atlas defaults to **SCRAM-SHA**.  
  
USERNAME

|

string

|

Required

|

Username that this resource deletes from the MongoDB database. This username
should be formatted as:

SCRAM-SHA

X.509

LDAP

AWS IAM

An alphanumeric string  
  
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

### Response Elements

This endpoint does not have response elements.

## Example Request

SCRAM-SHA

X.509

LDAP

AWS IAM

Delete one database user that Atlas authenticates using SCRAM-SHA and the
**admin** database.

## Important

You must modify the following code block with the appropriate credentials and
project ID.

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794dee37132bb7b/databaseUsers/admin/ellen"  
  
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

This endpoint doesn't return a response body.

What is MongoDB Atlas? →

