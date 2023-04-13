Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Project

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

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups  
      
  
### Request Path Parameters

This endpoint does not use HTTP request path parameters.

### Request Query Parameters

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
  
|

|

|  
  
|||  
  
projectOwnerId

|

string

|

Optional

|

Unique 24-hexadecimal digit string that identifies the Atlas user account to
be granted the `Project Owner` role on the specified project. If you set this
parameter, it overrides the default value of the oldest `Organization Owner`.  
  
### Request Body Parameters

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
name

|

string

|

Required

|

Name of the project to create.  
  
orgId

|

string

|

Required

|

Unique identifier of the organization within which to create the project. This
field is required when using API Key credentials.

## Important

To create a project using API Key credentials, you _must_ specify an `orgId`.
When you do, Atlas automatically selects the `Owner` of the specified
organization with the earliest account creation date and time as the `Project
Owner` for the newly created project.  
  
withDefaultAlertsSettings

|

Boolean

|

Optional

|

Flag that indicates whether to create the new project with the default alert
settings enabled. This parameter defaults to `true`.  
  
### Response Elements

Name

|

Type

|

Description  
  
||  
  
clusterCount

|

number

|

Quantity of Atlas clusters deployed in the project.  
  
created

|

string

|

ISO-8601-formatted timestamp of when Atlas created the project.  
  
id

|

string

|

Unique 24-hexadecimal digit string that identifies the project.  
  
links

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
name

|

string

|

Human-readable label that identifies the new project.  
  
orgId

|

string

|

Unique 24-hexadecimal digit string that identifies the Atlas organization to
which the project belongs.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups?projectOwnerId=a138a4bdb497e73460e70d04&pretty=true" \  
         --data '  
           {  
             "name" : "ProjectFoobar",  
             "orgId" : "5a0a1e7e0f2912c554080adc"  
           }'  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 201 Created  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    {  
      
      "clusterCount" : 0,  
      "created" : "2016-07-14T14:19:33Z",  
      "id" : "5a0a1e7e0f2912c554080ae6",  
      "links" : [],  
      "name" : "ProjectFoobar",  
      "orgId" : "5a0a1e7e0f2912c554080adc"  
    }  
  
What is MongoDB Atlas? →

