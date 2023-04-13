Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Project Settings

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Returns details about the settings for specified project. To learn more, see
Manage Project Settings.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You can successfully call this endpoint with the `Project Read Only` role.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/settings  
      
  
### Request Path Parameters

Path Element

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

Unique 24-hexadecimal digit string that identifies the project.  
  
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

### Response Elements

If you set the query element envelope to `true`, the response is wrapped by a
`content` object.

Name

|

Description  
  
|  
  
`isCollectDatabaseSpecificsStatisticsEnabled`

|

Flag that indicates whether statistics in cluster metrics collection is
enabled for the project.  
  
`isDataExplorerEnabled`

|

Flag that indicates whether Data Explorer is enabled for the project. If
enabled, you can query your database with an easy to use interface.  
  
`isPerformanceAdvisorEnabled`

|

Flag that indicates whether Performance Advisor and Profiler is enabled for
the project. If enabled, you can analyze database logs to recommend
performance improvements.  
  
`isRealtimePerformancePanelEnabled`

|

Flag that indicates whether Real Time Performance Panel is enabled for the
project. If enabled, you can see real time metrics from your MongoDB database.  
  
`isSchemaAdvisorEnabled`

|

Flag that indicates whether Schema Advisor is enabled for the project. If
enabled, you receive customized recommendations to optimize your data model
and enhance performance.  
  
## Example

### Request

    
    
    curl -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/settings"  
      
  
### Response

    
    
    {  
      
      "isCollectDatabaseSpecificsStatisticsEnabled":true,  
      "isDataExplorerEnabled":true,  
      "isPerformanceAdvisorEnabled":true,  
      "isRealtimePerformancePanelEnabled":true,  
      "isSchemaAdvisorEnabled":true  
    }  
  
What is MongoDB Atlas? →

