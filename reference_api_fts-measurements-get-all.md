Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Atlas Search Hardware and Status Metrics

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Measurement Values
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `fts` resource allows you to return all the Atlas Search hardware and
status metrics for one process in the specified project.

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

    
    
    GET /groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics/measurements  
      
  
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
  
`end`

|

string

|

Conditional

|

Required if you don't specify `period`. Timestamp in ISO 8601 date and time
format in UTC that indicates the end date up to which Atlas reports the
metrics. If you specify **end** you must also specify **start**. Mutually
exclusive with **period**.

|  
  
`envelope`

|

boolean

|

Optional

|

Flag that indicates whether Atlas should wrap the response in a JSON envelope.

If API clients cannot access the HTTP response headers or status code, set
`envelope=true` in the query.

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
  
For endpoints that return a list of results, the **results** object is an
envelope. Atlas adds the **status** field to the response body.

`false`  
  
`granularity`

|

string

|

Required

|

Duration in ISO 8601 notation that specifies the interval at which Atlas
reports the metrics. Atlas supports the following subset of ISO 8601-formatted
time periods:

  *  **PT10S**

## Note

Atlas supports a 10 second granularity only on `M40` and larger clusters. To
learn more, see Premium Monitoring Granularity.

  *  **PT1M**

  *  **PT5M**

  *  **PT1H**

  *  **P1D**

When you specify **granularity** , you must specify either **period** _or_
**start** and **end**.

|  
  
`metrics`

|

string

|

Optional

|

List that contains the metrics that you want Atlas to report for the
associated data series. If you don't specify individual **metrics** , the
endpoint returns all metrics for the associated data series.

|

`<all-metrics>`  
  
`period`

|

string

|

Conditional

|

Required if you don't specify `start` and `end`. Duration in ISO 8601 notation
that specifies the length of time over which Atlas reports the metrics.
Mutually exclusive with `start` and `end`.

## Example

To request the last 36 hours, specify: `period=P1DT12H`.

|  
  
`start`

|

string

|

Conditional

|

Required if you don't specify `period`. Timestamp in ISO 8601 date and time
format in UTC that indicates the start date from which Atlas reports the
metrics. If you specify **start** you must also specify **end**. Mutually
exclusive with **period**.

|  
  
### Request Body Parameters

This endpoint doesn't use HTTP request body parameters.

## Response Elements

The HTTP response returns a JSON document that includes an a array of Atlas
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
  
`granularity`

|

string

|

Duration in ISO 8601 notation that specifies the interval at which Atlas
reports the metrics.  
  
`start`

|

string

|

Timestamp in ISO 8601 date and time format in UTC that indicates the start
date from which Atlas reports the metrics.  
  
`end`

|

string

|

Timestamp in ISO 8601 date and time format in UTC that indicates the end date
up to which Atlas reports the metrics.  
  
`hardwareMeasurements`

|

array

|

List that contains all available Atlas Search hardware metrics.  
  
`hardwareMeasurements.dataPoints`

|

string

|

List that contains Atlas Search hardware metric data.  
  
`hardwareMeasurements.dataPoints.timestamp`

|

string

|

Timestamp in ISO 8601 date and time format in UTC that indicates when Atlas
captured the Atlas Search hardware metric data point.  
  
`hardwareMeasurements.dataPoints.value`

|

number

|

Number that indicates the Atlas Search hardware metric data point value.  
  
`hardwareMeasurements.name`

|

string

|

Human-readable label that identifies the Atlas Search hardware metric.  
  
`hardwareMeasurements.units`

|

string

|

Unit of measurement that applies to the Atlas Search hardware metric.  
  
`statusMeasurements`

|

array

|

List that contains all available Atlas Search status metrics.  
  
`statusMeasurements.dataPoints`

|

string

|

List that contains Atlas Search status metric data.  
  
`statusMeasurements.dataPoints.timestamp`

|

string

|

Timestamp in ISO 8601 date and time format in UTC that indicates when Atlas
captured the Atlas Search status metric data point.  
  
`statusMeasurements.dataPoints.value`

|

number

|

Number that indicates the Atlas Search status metric data point value.  
  
`statusMeasurements.name`

|

string

|

Human-readable label that identifies the Atlas Search status metric.  
  
`statusMeasurements.units`

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
  
### Measurement Values

Measurement

|

Description  
  
|  
  
`FTS_DISK_USAGE`

|

Total bytes of disk space that search processes use.  
  
`FTS_PROCESS_CPU_KERNEL`

|

Percentage of time that the CPU spent servicing operating system calls for the
search process. For servers with more than 1 CPU core, this value can exceed
100%.  
  
`FTS_PROCESS_CPU_USER`

|

Percentage of time that the CPU spent servicing the search process. For
servers with more than 1 CPU core, this value can exceed 100%.  
  
`FTS_PROCESS_NORMALIZED_CPU_KERNEL`

|

Percentage of time that the CPU spent servicing operating system calls for the
search process, scaled to a range of 0-100% by dividing by the number of CPU
cores.  
  
`FTS_PROCESS_NORMALIZED_CPU_USER`

|

Percentage of time that the CPU spent servicing the search process, scaled to
a range of 0-100% by dividing by the number of CPU cores.  
  
`FTS_PROCESS_RESIDENT_MEMORY`

|

Total bytes of resident memory that search processes occupy.  
  
`FTS_PROCESS_SHARED_MEMORY`

|

Total bytes of shared memory that search processes occupy.  
  
`FTS_PROCESS_VIRTUAL_MEMORY`

|

Total bytes of virtual memory that search processes occupy.  
  
`JVM_CURRENT_MEMORY`

|

Amount of memory that the JVM heap is currently using.  
  
`JVM_MAX_MEMORY`

|

Total available memory in the JVM heap.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics/measurements?granularity=PT1M&period=PT1M"  
  
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
      
     "end": "2021-12-20T16:50:48Z",  
     "granularity": "PT1M",  
     "groupId": "5f86fb2ff9c4e56d39502559",  
     "hardwareMeasurements": [  
         {  
             "dataPoints": [  
                 {  
                     "timestamp": "2021-12-20T16:50:48Z",  
                     "value": 39354368  
                 }  
             ],  
             "name": "FTS_DISK_USAGE",  
             "units": "BYTES"  
         },  
         {  
             "dataPoints": [  
                 {  
                     "timestamp": "2021-12-20T16:50:48Z",  
                     "value": null  
                 }  
             ],  
             "name": "FTS_PROCESS_CPU_USER",  
             "units": "PERCENT"  
         },  
         {  
             "dataPoints": [  
                 {  
                     "timestamp": "2021-12-20T16:50:48Z",  
                     "value": null  
                 }  
             ],  
             "name": "FTS_PROCESS_CPU_KERNEL",  
             "units": "PERCENT"  
         },  
         {  
             "dataPoints": [  
                 {  
                     "timestamp": "2021-12-20T16:50:48Z",  
                     "value": null  
                 }  
             ],  
             "name": "FTS_PROCESS_NORMALIZED_CPU_USER",  
             "units": "PERCENT"  
         },  
         {  
             "dataPoints": [  
                 {  
                     "timestamp": "2021-12-20T16:50:48Z",  
                     "value": null  
                 }  
             ],  
             "name": "FTS_PROCESS_NORMALIZED_CPU_KERNEL",  
             "units": "PERCENT"  
         },  
         {  
             "dataPoints": [  
                 {  
                     "timestamp": "2021-12-20T16:50:48Z",  
                     "value": 389877760  
                 }  
             ],  
             "name": "FTS_PROCESS_RESIDENT_MEMORY",  
             "units": "BYTES"  
         },  
         {  
             "dataPoints": [  
                 {  
                     "timestamp": "2021-12-20T16:50:48Z",  
                     "value": 3353886720  
                 }  
             ],  
             "name": "FTS_PROCESS_VIRTUAL_MEMORY",  
             "units": "BYTES"  
         },  
         {  
             "dataPoints": [  
                 {  
                     "timestamp": "2021-12-20T16:50:48Z",  
                     "value": 15740928  
                 }  
             ],  
             "name": "FTS_PROCESS_SHARED_MEMORY",  
             "units": "BYTES"  
         }  
     ],  
     "links": [  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5f86fb2ff9c4e56d39502559/hosts/cluster0-shard-00-00.5f3gk.mongodb.net:27017/fts/metrics/measurements?granularity=PT1M&period=PT1M",  
             "rel": "self"  
         },  
         {  
             "href": "https://cloud-dev.mongodb.com/api/atlas/v1.0/groups/5f86fb2ff9c4e56d39502559/processes/cluster0-shard-00-00.5f3gk.mongodb.net:27017",  
             "rel": "http://cloud.mongodb.com/host"  
         }  
     ],  
     "processId": "cluster0-shard-00-00.5f3gk.mongodb.net:27017",  
     "start": "2021-12-20T16:50:48Z",  
     "statusMeasurements": [  
         {  
             "dataPoints": [],  
             "name": "JVM_CURRENT_MEMORY",  
             "units": "MEGABYTES"  
         },  
         {  
             "dataPoints": [],  
             "name": "JVM_MAX_MEMORY",  
             "units": "MEGABYTES"  
         }  
     ]  
    }  
  
What is MongoDB Atlas? →

