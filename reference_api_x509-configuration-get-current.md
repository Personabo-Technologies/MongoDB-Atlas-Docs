Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Current X.509 Configuration

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request
  * Path Parameters
  * Query Parameters
  * Body Parameters
  * Response
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Get the current customer-managed X.509 configuration details for an Atlas
project.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Required Roles

You must have the `Atlas admin` role to use this endpoint.

## Resource

## Note

X.509 configurations and LDAP configurations are managed using the same
resource. Requests to the resource will return both configuration objects.

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/userSecurity  
      
  
## Request

### Path Parameters

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`GROUP-ID`

|

string

|

Required

|

Identifier for the Atlas project associated with the X.509 configuration.  
  
### Query Parameters

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
  
### Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
`ldap`

|

object

|

LDAP configuration for an Atlas project. To learn more about LDAP
configuration options, see Get Current LDAP Configuration.  
  
`customerX509`

|

object

|

Customer-managed X.509 configuration for an Atlas project.  
  
`customerX509.cas`

|

string

|

PEM string containing one or more customer CAs for database user
authentication.  
  
## Example

### Request

The following example returns the current X.509 configuration details for an
Atlas project.

    
    
    curl --request GET \  
      
      --user "{publicApiKey}:{privateApiKey}" \  
      --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/userSecurity?pretty=true"  
  
### Response

The following partial example shows the JSON document returned:

    
    
    1| {  
    |  
    2|    "ldap" : {},  
    3|    "customerX509" : {  
    4|      "cas" : "--BEGIN CERTIFICATE--\nMIICwjCCAaoCCQDUd  
    5|      +4L8xlyXTANBgkqhkiG9w0BAQsFADAjMQ8wDQYDVQQDDAZy\nb290Q0ExEDAOBgN  
    6|      ...  
    7|      +4IGl7MBfZ\nlpJl7/in79pUyXII907ZJNr6ghIXDbO1luVIXv7yyV13uDiw/  
    8|      dA=\n--END CERTIFICATE--\n"  
    9|    }  
    10| }  
  
What is MongoDB Atlas? →

