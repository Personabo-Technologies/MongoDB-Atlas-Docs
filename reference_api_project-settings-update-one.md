Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update One Project Settings

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

Updates the settings for the specified project. To learn more, see Manage
Project Settings.

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

You can successfully call this endpoint with the `Project Owner` role.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    PATCH /groups/{GROUP-ID}/settings  
      
  
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

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`isCollectDatabaseSpecificsStatisticsEnabled`

|

boolean

|

Optional

|

Flag that indicates whether to enable statistics in cluster metrics collection
for the project.  
  
`isDataExplorerEnabled`

|

boolean

|

Optional

|

Flag that indicates whether to enable Data Explorer for the project. If
enabled, you can query your database with an easy to use interface.

## Important

When Data Explorer is disabled, you cannot:

  * Terminate slow operations from the Real-Time Performance Panel.

  * Create indexes from the Performance Advisor. You can still view Performance Advisor recommendations, but you must create those indexes from `mongosh`.

  
  
`isPerformanceAdvisorEnabled`

|

boolean

|

Optional

|

Flag that indicates whether to enable Performance Advisor and Profiler for the
project. If enabled, you can analyze database logs to recommend performance
improvements.  
  
`isRealtimePerformancePanelEnabled`

|

boolean

|

Optional

|

Flag that indicates whether to enable Real Time Performance Panel for the
project. If enabled, you can see real time metrics from your MongoDB database.  
  
`isSchemaAdvisorEnabled`

|

boolean

|

Optional

|

Flag that indicates whether to enable Schema Advisor for the project. If
enabled, you receive customized recommendations to optimize your data model
and enhance performance. Disable this setting to disable schema suggestions in
the Performance Advisor and the Data Explorer.  
  
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

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
      --header "Accept: application/json" \  
      --header "Content-Type: application/json" \  
      --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/settings" \  
       --data '  
        {  
          "isCollectDatabaseSpecificsStatisticsEnabled":false,  
          "isDataExplorerEnabled":true,  
          "isPerformanceAdvisorEnabled":true,  
          "isRealtimePerformancePanelEnabled":true,  
          "isSchemaAdvisorEnabled":true  
        }'  
  
### Response

    
    
    {  
      
      "isCollectDatabaseSpecificsStatisticsEnabled":false,  
      "isDataExplorerEnabled":true,  
      "isPerformanceAdvisorEnabled":true,  
      "isRealtimePerformancePanelEnabled":true,  
      "isSchemaAdvisorEnabled":true  
    }  
  
What is MongoDB Atlas? →

