Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Auditing Configuration for a Project

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/auditLog  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required.

|

The unique identifier for the project.  
  
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

This endpoint does not use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
`auditAuthorizationSuccess`

|

boolean

|

Indicates whether the auditing system captures successful authentication
attempts for audit filters using the `"atype" : "authCheck"` auditing event.
For more information, see auditAuthorizationSuccess  
  
`auditFilter`

|

string

|

JSON-formatted audit filter used by the project  
  
`configurationType`

|

string

|

Denotes the configuration method for the audit filter. Possible values are:

  * `NONE` \- auditing not configured for the project.

  * `FILTER_BUILDER` \- auditing configured via Atlas UI filter builder

  * `FILTER_JSON` \- auditing configured via Atlas custom filter or API

  
  
`enabled`

|

boolean

|

Denotes whether or not the project associated with the `{GROUP-ID}` has
database auditing enabled.  
  
## Example Request

    
    
    curl -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
     --header "Accept: application/json" \  
     --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/auditLog?pretty=true"  
  
## Example Response

    
    
    {  
      
        "auditAuthorizationSuccess": false,  
        "auditFilter": "{\n  \"atype\": \"authenticate\",\n  \"param\": {\n    \"user\": \"auditAdmin\",\n    \"db\": \"admin\",\n    \"mechanism\": \"SCRAM-SHA-1\"\n  }\n}",  
        "configurationType": "FILTER_JSON",  
        "enabled": true  
    }  
  
What is MongoDB Atlas? →

