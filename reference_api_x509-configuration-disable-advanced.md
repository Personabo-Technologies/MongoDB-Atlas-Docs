Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Disable Customer-Managed X.509

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

Clear customer-managed X.509 settings on a project, including the uploaded
Certificate Authority, disabling Self-Managed X.509.

## Important

### Disabling customer-managed X.509 triggers a rolling restart.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Required Roles

You must have the `Atlas admin` role to use this endpoint.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    DELETE /groups/{GROUP-ID}/userSecurity/customerX509  
      
  
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

Customer-managed X.509 configuration for an Atlas project. Empty if the
operation was successful.  
  
## Example

### Request

The following example clears customer-managed X.509 settings on a project,
including the uploaded Certificate Authority, disabling customer-managed
X.509.

    
    
    curl --request DELETE \  
      
    --user "{publicApiKey}:{privateApiKey}" \  
    --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/userSecurity/customerX509"  
  
### Response

The following example shows the JSON document returned:

    
    
    {  
      
      "customerX509" : {},  
      "ldap" : {  
        "authenticationEnabled" : false,  
        "authorizationEnabled" : false,  
        "userToDNMapping" : null  
      }  
    }  
  
What is MongoDB Atlas? →

