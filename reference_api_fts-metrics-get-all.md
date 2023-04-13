Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Atlas Search Metric Types

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Parameters
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

The `fts` resource allows you to return all the Atlas Search metric types for
one process in the specified project.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Required Roles

You must have the `Project Read Only` or higher role to view the Atlas Search
metric types using the Atlas UI or API.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics  
      
  
## Request Parameters

### Request Path Parameters

Path Element

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

Unique 24-hexadecimal digit string that identifies the project.  
  
`PROCESS-ID`

|

string

|

Required

|

Unique hexadecimal digit string, or a string in the form of `<hostname>:port`,
that identifies the process.

## Note

You can find the `PROCESS-ID` in the URL of the process in Atlas after
`/host/`.  
  
### Request Query Parameters

|

|

|  
  
|||  
  
Name

|

Type

|

Description

|

Default  
  
`envelope`

|

boolean

|

Indicates whether or not to wrap the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

For endpoints that return one result, response body includes:

|

`status`

|

HTTP response code  
  
|  
  
`envelope`

|

The expected response body  
  
For endpoints that return a list of results, the `results` object is an
envelope. Atlas adds the `status` field to the response body.

`false`  
  
### Request Body Parameters

This endpoint doesn't use HTTP request body parameters.

## Response Elements

The HTTP response returns a JSON document that includes an array of Atlas
Search metric types. Each Atlas Search metric type contains the following
elements:

Name

|

Type

|

Description  
  
||  
  
`groupId`

|

string

|

Unique 24-hexadecimal digit string that identifies the project.  
  
`processId`

|

string

|

String in the form of `<hostname>:port` that identifies the process.  
  
`hardwareMetrics`

|

array

|

List that contains all available Atlas Search hardware metrics.  
  
`hardwareMetrics.metricName`

|

string

|

Human-readable label that identifies the Atlas Search hardware metric.  
  
`hardwareMetrics.units`

|

string

|

Unit of measurement that applies to the Atlas Search hardware metric.  
  
`indexMetrics`

|

array

|

List that contains all available Atlas Search index metrics.  
  
`indexMetrics.metricName`

|

string

|

Human-readable label that identifies the Atlas Search index metric.  
  
`indexMetrics.units`

|

string

|

Unit of measurement that applies to the Atlas Search index metric.  
  
`statusMetrics`

|

array

|

List that contains all available Atlas Search status metrics.  
  
`statusMetrics.metricName`

|

string

|

Human-readable label that identifies the Atlas Search status metric.  
  
`statusMetrics.units`

|

string

|

Unit of measurement that applies to the Atlas Search status metric.  
  
`links`

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics"  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

The following example response contains an array of Atlas Search metric types.

    
    
    {  
      
     "groupId": "5f86fb2ff9c4e56d39502559",  
     "hardwareMetrics": [  
         {  
             "metricName": "FTS_DISK_USAGE",  
             "units": "BYTES"  
         },  
         {  
             "metricName": "FTS_PROCESS_CPU_USER",  
             "units": "PERCENT"  
         },  
         {  
             "metricName": "FTS_PROCESS_CPU_KERNEL",  
             "units": "PERCENT"  
         },  
         {  
             "metricName": "FTS_PROCESS_NORMALIZED_CPU_USER",  
             "units": "PERCENT"  
         },  
         {  
             "metricName": "FTS_PROCESS_NORMALIZED_CPU_KERNEL",  
             "units": "PERCENT"  
         },  
         {  
             "metricName": "FTS_PROCESS_RESIDENT_MEMORY",  
             "units": "BYTES"  
         },  
         {  
             "metricName": "FTS_PROCESS_VIRTUAL_MEMORY",  
             "units": "BYTES"  
         },  
         {  
             "metricName": "FTS_PROCESS_SHARED_MEMORY",  
             "units": "BYTES"  
         }  
     ],  
     "indexMetrics": [  
         {  
             "metricName": "REPLICATION_LAG",  
             "units": "SECONDS"  
         },  
         {  
             "metricName": "NUMBER_OF_SUCCESS_QUERIES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "metricName": "NUMBER_OF_ERROR_QUERIES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "metricName": "TOTAL_NUMBER_OF_QUERIES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "metricName": "NUMBER_OF_GETMORE_COMMANDS",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "metricName": "NUMBER_OF_INSERTS",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "metricName": "NUMBER_OF_UPDATES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "metricName": "NUMBER_OF_DELETES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "metricName": "INDEX_SIZE_ON_DISK",  
             "units": "MEGABYTES"  
         },  
         {  
             "metricName": "NUMBER_OF_INDEX_FIELDS",  
             "units": "SCALAR"  
         }  
     ],  
     "links": [  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5f86fb2ff9c4e56d39502559/processes/4d5ef1b285f7c73f4e9e24f0abd400b2",  
             "rel": "http://mms.mongodb.com/host"  
         },  
         {  
             "href": "https://cloud.mongodb.com/api/public/v1.0/groups/5f86fb2ff9c4e56d39502559",  
             "rel": "http://mms.mongodb.com/group"  
         }  
     ],  
     "processId": "4d5ef1b285f7c73f4e9e24f0abd400b2",  
     "statusMetrics": [  
         {  
             "metricName": "JVM_CURRENT_MEMORY",  
             "units": "MEGABYTES"  
         },  
         {  
             "metricName": "JVM_MAX_MEMORY",  
             "units": "MEGABYTES"  
         }  
     ]  
    }  
  
What is MongoDB Atlas? →

