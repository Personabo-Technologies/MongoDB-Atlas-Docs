Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete a Configuration for a Third-Party Service Integration

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
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

## Important

Deleting an integration from a project removes that integration configuration
only for that project. This does not affect any other project or
organization's configured `{INTEGRATION-TYPE}` integrations.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    DELETE /groups/{GROUP-ID}/integrations/{INTEGRATION-TYPE}  
      
  
### Request Path Parameters

Parameter

|

Required/Optional

|

Description  
  
||  
  
`{GROUP-ID}`

|

Required

|

Project identifier.  
  
`{INTEGRATION-TYPE}`

|

Required

|

Third-party service integration identifier. Accepted values are:

  * `PAGER_DUTY`

  * `SLACK`

  * `DATADOG`

  * `NEW_RELIC`

  * `OPS_GENIE`

  * `VICTOR_OPS`

  * `FLOWDOCK`

  * `WEBHOOK`

  * `MICROSOFT_TEAMS`

  * `PROMETHEUS`

  
  
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

## Response Elements

This endpoint does not have response elements.

## Example Request

    
    
    curl -X DELETE -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/5d791c84ff7a2522cc4f9aa1/integrations/DATADOG"  
      
  
## Example Response

This endpoint doesn't return a response body.

What is MongoDB Atlas? →

