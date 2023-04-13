Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Atlas Search Index Metrics

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

The `fts` resource allows you to return all the Atlas Search index metrics for
a namespace on the specified process.

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

    
    
    GET /groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics/indexes/{DATABASE-NAME}/{COLLECTION-NAME}/measurements  
      
  
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
  
`DATABASE-NAME`

|

string

|

Required

|

Human-readable label that identifies the database.  
  
`COLLECTION-NAME`

|

string

|

Required

|

Human-readable label that identifies the collection.  
  
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

If API clients can't access the HTTP response headers or status code, set
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
  
`collectionName`

|

string

|

Human-readable label that identifies the collection.  
  
`databaseName`

|

string

|

Human-readable label that identifies the database.  
  
`granularity`

|

string

|

Duration in ISO 8601 notation that specifies the interval at which Atlas
reports the metrics.  
  
`groupId`

|

string

|

Unique 24-hexadecimal digit string that identifies the project.  
  
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
  
`indexIds`

|

array

|

List that contains the unique 24-hexadecimal digit strings that identifies the
indexes.  
  
`indexStatsMeasurements`

|

array

|

List that contains all available Atlas Search index metrics.  
  
`indexStatsMeasurements.dataPoints`

|

string

|

List that contains Atlas Search index metric data.  
  
`indexStatsMeasurements.dataPoints.timestamp`

|

string

|

Timestamp in ISO 8601 date and time format in UTC that indicates when Atlas
captured the Atlas Search index metric data point.  
  
`indexStatsMeasurements.dataPoints.value`

|

number

|

Number that indicates the Atlas Search index metric data point value.  
  
`indexStatsMeasurements.name`

|

string

|

Human-readable label that identifies the Atlas Search index metric.  
  
`indexStatsMeasurements.units`

|

string

|

Unit of measurement that applies to the Atlas Search index metric.  
  
`links`

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
`processId`

|

string

|

String in the form of `<hostname>:port` that identifies the process.  
  
### Measurement Values

Measurement

|

Description  
  
|  
  
`REPLICATION_LAG`

|

Approximate number of seconds Atlas Search is behind in replicating changes
from the oplog of `mongod`.  
  
`NUMBER_OF_SUCCESS_QUERIES`

|

Total number of queries that successfully returned a response.  
  
`NUMBER_OF_ERROR_QUERIES`

|

Total number of queries that were unable to return a response.  
  
`TOTAL_NUMBER_OF_QUERIES`

|

Total number of queries submitted to Atlas Search.  
  
`NUMBER_OF_GETMORE_COMMANDS`

|

Total number of `getmore` commands run on all Atlas Search queries.  
  
`NUMBER_OF_INSERTS`

|

Total number of documents or fields defined in the index definition indexed
into Atlas Search.  
  
`NUMBER_OF_UPDATES`

|

Total number of documents or fields defined in the index definition updated in
Atlas Search.  
  
`NUMBER_OF_DELETES`

|

Total number of documents or fields defined in the index definition removed
from Atlas Search.  
  
`INDEX_SIZE_ON_DISK`

|

Total size of the index.  
  
`NUMBER_OF_INDEX_FIELDS`

|

Total number of unque fields present in the Atlas Search index.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics/indexes/{DATABASE-NAME}/{COLLECTION-NAME}/measurements?granularity=PT1M&period=PT1M"  
  
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
      
     "collectionName": "movies",  
     "databaseName": "sample_mflix",  
     "granularity": "PT1M",  
     "groupId": "5f86fb2ff9c4e56d39502559",  
     "indexIds": [],  
     "indexStatsMeasurements": [  
         {  
             "dataPoints": [],  
             "name": "REPLICATION_LAG",  
             "units": "SECONDS"  
         },  
         {  
             "dataPoints": [],  
             "name": "NUMBER_OF_SUCCESS_QUERIES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "dataPoints": [],  
             "name": "NUMBER_OF_ERROR_QUERIES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "dataPoints": [],  
             "name": "TOTAL_NUMBER_OF_QUERIES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "dataPoints": [],  
             "name": "NUMBER_OF_GETMORE_COMMANDS",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "dataPoints": [],  
             "name": "NUMBER_OF_INSERTS",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "dataPoints": [],  
             "name": "NUMBER_OF_UPDATES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "dataPoints": [],  
             "name": "NUMBER_OF_DELETES",  
             "units": "SCALAR_PER_SECOND"  
         },  
         {  
             "dataPoints": [],  
             "name": "INDEX_SIZE_ON_DISK",  
             "units": "MEGABYTES"  
         },  
         {  
             "dataPoints": [],  
             "name": "NUMBER_OF_INDEX_FIELDS",  
             "units": "SCALAR"  
         }  
     ],  
     "links": [  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5f86fb2ff9c4e56d39502559/hosts/4d5ef1b285f7c73f4e9e24f0abd400b2/fts/metrics/indexes/sample_mflix/movies/measurements?granularity=PT1M&period=PT1M",  
             "rel": "self"  
         },  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5f86fb2ff9c4e56d39502559/processes/cluster0-shard-00-00.5f3gk.mongodb-dev.net:27017",  
             "rel": "http://cloud.mongodb.com/host"  
         }  
     ],  
     "processId": "cluster0-shard-00-00.5f3gk.mongodb-dev.net:27017"  
    }  
  
What is MongoDB Atlas? →

