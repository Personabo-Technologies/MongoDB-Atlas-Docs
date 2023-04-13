Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Slow Queries

Share Feedback

On this page

  * Resource
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

Return log lines for slow queries as determined by the Performance Advisor and
Query Profiler.

## Note

Users without one of the following roles cannot successfully call the
endpoint:

  * `Project Owner` access

  * `Project Data Access Admin` access

  * `Project Data Access Read/Write` access

  * `Project Data Access Read Only` access

The other Performance Advisor endpoints allow users without these roles to
call the endpoints and receive redacted data.

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

## Resource

    
    
    GET /groups/{GROUP-ID}/processes/{PROCESS-ID}/performanceAdvisor/slowQueryLogs  
      
  
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

String

|

Required

|

Unique 24-hexadecimal digit string that identifies the project in which you
find the desired process.  
  
PROCESS-ID

|

String

|

Required

|

Atlas hostname and port that hosts the desired MongoDB process.

## Example

m10-shard-00-00-17jcm.mongodb.net:27017

To retrieve all processes in the project with a given **GROUP-ID** , use the
/groups/{GROUP-ID}/processes endpoint.  
  
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

|  
  
||||  
  
since

|

number

|

Optional

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch from
which to retrieve slow queries.

|  
  
duration

|

number

|

Optional

|

Length of time in milliseconds during which to find slow queries among the
managed namespaces in the cluster.

|  
  
namespaces

|

string

|

Optional

|

Namespaces from which to retrieve slow queries. A namespace consists of the
database and collection resource separated by a `.`, such as
`<database>.<collection>`.

To specify multiple namespaces, pass the parameter multiple times using an
ampersand (`&`) as a delimiter, once for each namespace.

## Example

?namespaces=data.stocks&namespaces=data.zips&pretty=true

Omit to return results for all namespaces.

|  
  
`nLogs`

|

number

|

Optional

|

Maximum number of log lines to return.

|

`20000`  
  
## Note

  * If you specify **since** and omit **duration** , the response contains results from the **since** point up to and including the present time.

  * If you specify **duration** and omit **since** , the response contains results from **duration** ms ago up to and including the present time.

  * If you omit both **since** and **duration** , the response contains results from the previous 24 hours up up to and including the present time.

### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
`slowQueries`

|

array of documents

|

A list of documents with information about slow queries as detected by the
Performance Advisor.  
  
`slowQueries[n].line`

|

string

|

The raw log line pertaining to the slow query.  
  
`slowQueries[n].namespace`

|

string

|

The namespace in which the slow query ran.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest -i \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/processes/{PROCESS-ID}/performanceAdvisor/slowQueryLogs?namespaces=myDb.users&pretty=true"  
  
## Example Response

    
    
    {  
      
      "slowQueries" : [ {  
        "line" : "2018-08-16T22:53:43.447+0000 I COMMAND  [conn10614] command myDb.users appName: \"MongoDB Shell\" command: find { find: \"users\", filter: { emails: \"tocde@fijoow.to\" }, lsid: { id: UUID(\"832b4b0e-085a-480e-b470-16a0994dc7cb\") }, $clusterTime: { clusterTime: Timestamp(1534460016, 1)...",  
       "namespace" : "myDb.users"  
      }, {  
        "line" : "2018-08-16T22:54:32.705+0000 I COMMAND  [conn10614] command myDb.users appName: \"MongoDB Shell\" command: find { find: \"users\", filter: { emails: \"la@sa.kp\" }, lsid: { id: UUID(\"832b4b0e-085a-480e-b470-16a0994dc7cb\") }, $clusterTime: { clusterTime: Timestamp(1534460056, 1), ...",  
        "namespace" : "myDb.users"  
      } ]  
    }  
  
What is MongoDB Atlas? →

