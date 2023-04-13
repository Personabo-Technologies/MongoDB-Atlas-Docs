Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Measurements of a Disk for a MongoDB Process

Share Feedback

On this page

  * Resource
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

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Retrieve measurements of a disk or partition for a specific MongoDB process.
An Atlas MongoDB process can be either a `mongod` or `mongos`.

## Note

To calculate some metric series, Atlas takes the rate between every two
adjacent points. For these metric series, the first data point has a null
value because Atlas can't calculate a rate for the first data point given the
query time range.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/processes/{HOST}:{PORT}/disks/{DISK-NAME}/measurements  
      
  
### Request Path Parameters

Parameter

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

Unique 24-hexadecimal digit string that identifies the project that owns this
Atlas MongoDB process.  
  
HOST

|

string

|

Required

|

Hostname, FQDN, IPv4 address, or IPv6 address of the machine running the Atlas
MongoDB process.  
  
PORT

|

number

|

Required

|

IANA port to which the Atlas MongoDB process listens.  
  
|

|

|  
  
|||  
  
DISK-NAME

|

string

|

Required

|

Label that identifies the disk or partition from which you want to retrieve
measurements.  
  
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
  
pageNum

|

integer

|

Optional

|

Page number, starting with one, that Atlas returns of the total number of
objects.

|

`1`  
  
itemsPerPage

|

integer

|

Optional

|

Number of items that Atlas returns per page, up to a maximum of 500.

|

`100`  
  
includeCount

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the **totalCount** parameter in the
response body.

|

`true`  
  
pretty

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the JSON response in the prettyprint
format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag that indicates whether Atlas wraps the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

Endpoints that return a list of results use the **results** object as an
envelope. Atlas adds the **status** parameter to the response body.

|

`false`  
  
|

|

|

|  
  
||||  
  
granularity

|

string

|

Required

|

Duration in ISO 8601 notation that specifies the interval between measurement
data points.

## Example

 **PT1M** specifies 1-minute granularity.

Atlas supports the following subset of ISO 8601-formatted time periods:

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

Atlas retrieves database metrics every 20 minutes by default. Results include
data points with 20 minute intervals.

To learn more, see Review MongoDB Processes.

|  
  
period

|

string

|

Required

|

Duration in ISO 8601 notation that specifies the length of time in the past to
query. Mutually exclusive with **start** and **end**.

## Example

To request the last 36 hours, specify: **period=P1DT12H**.

|  
  
start

|

string

|

Required

|

Date and time that specifies when to start retrieving measurements. If you set
**start** , you must set **end**. You can't set this parameter and **period**
in the same request. This parameter expresses its value in the RFC 3339
timestamp format in UTC.

|  
  
end

|

string

|

Required

|

Date and time that specifies when to stop retrieving measurements. If you set"
**end** , you must set **start**. You can't set this parameter and" **period**
in the same request. This parameter expresses its value in the RFC 3339
timestamp format in UTC.

|  
  
m

|

string

|

Optional

|

Type of measurements this endpoint return. If you don't set **m** , the
endpoint returns all measurements.

To specify multiple values for **m** , you must repeat the **m** parameter.

## Example

    
    
    | ../measurements?m=<measurement>&m=<measurement>&m=...  
      
  
You must specify measurements that are valid for the host. Atlas returns an
error if any specified measurements are invalid.

The Measurement Values section details these metrics.  
  
### Request Body Parameters

This endpoint doesn't use HTTP request body parameters.

## Response Elements

## Important

### Limited Metrics for Free/Shared Tier Clusters

 **M0/M2/M5** clusters return a subset of the metrics documented.

If you set the query parameter to **envelope=true** , the resource wraps the
response in a **content** object.

The HTTP response returns a JSON document that includes the following objects:

Name

|

Type

|

Description  
  
||  
  
end

|

string

|

Date and time that specifies when to stop retrieving measurements. If you set"
**end** , you must set **start**. You can't set this parameter and" **period**
in the same request. This parameter expresses its value in the RFC 3339
timestamp format in UTC.  
  
granularity

|

string

|

Duration in ISO 8601 notation that specifies the interval between measurement
data points.  
  
groupId

|

string

|

Unique 24-hexadecimal digit string that identifies the project that owns the
Atlas MongoDB process.  
  
hostId

|

string

|

Hostname and port of the host running the Atlas MongoDB process.  
  
links

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
measurements

|

array

|

List of measurements recorded and their data points.  
  
measurements.dataPoints

|

array

|

Value of and metadata provided for one data point. If Atlas has no data point
for a particular moment in time, the **value** field is set to **null**.  
  
measurements.dataPoints.timestamp

|

string

|

Timestamp in ISO 8601 date and time format in UTC when this time interval that
this data point represents began.  
  
measurements.dataPoints.value

|

number

|

Value this data point provides.  
  
measurements.name

|

string

|

Name of the measurement that this data point covers.

The Measurement Values section details these metrics.  
  
measurements.units

|

string

|

Magnitude by which Atlas quanitifies the measurement.  
  
processId

|

string

|

Hostname and port of the machine running the Atlas MongoDB process.  
  
start

|

string

|

Date and time that specifies when to start retrieving measurements. If you set
**start** , you must set **end**. You can't set this parameter and **period**
in the same request. This parameter expresses its value in the RFC 3339
timestamp format in UTC.  
  
|

|  
  
||  
  
partitionName

|

string

|

Name of the disk or partition to which the measurements apply.  
  
### Measurement Values

|  
  
|  
  
DISK_PARTITION_IOPS_READ

MAX_DISK_PARTITION_IOPS_READ

DISK_PARTITION_IOPS_WRITE

MAX_DISK_PARTITION_IOPS_WRITE

DISK_PARTITION_IOPS_TOTAL

MAX_DISK_PARTITION_IOPS_TOTAL

|

Measures throughput of I/O operations for the disk partition used for MongoDB.  
  
DISK_PARTITION_UTILIZATION

MAX_DISK_PARTITION_UTILIZATION

|

The percentage of time during which requests are being issued to and serviced
by the partition. This includes requests from any process, not just MongoDB
processes.  
  
DISK_PARTITION_LATENCY_READ

MAX_DISK_PARTITION_LATENCY_READ

DISK_PARTITION_LATENCY_WRITE

MAX_DISK_PARTITION_LATENCY_WRITE

|

Measures latency per operation type of the disk partition used by MongoDB.  
  
DISK_PARTITION_SPACE_FREE

MAX_DISK_PARTITION_SPACE_FREE

DISK_PARTITION_SPACE_USED

MAX_DISK_PARTITION_SPACE_USED

DISK_PARTITION_SPACE_PERCENT_FREE

MAX_DISK_PARTITION_SPACE_PERCENT_FREE

DISK_PARTITION_SPACE_PERCENT_USED

MAX_DISK_PARTITION_SPACE_PERCENT_USED

|

Measures the free disk space and used disk space on the disk partition used by
MongoDB.  
  
## Example Request

Replace the information in brackets `{}` with your own Atlas information to
execute this example request:

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Content-Type: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/processes/{HOST}:{PORT}/disks/{DISK-NAME}/measurements?granularity=PT1M&period=PT1M&pretty=true"  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    1| {  
    |  
    2|    "end":"2021-04-09T18:07:45Z",  
    3|    "granularity":"PT1M",  
    4|    "groupId":"48c769055fd770eb6e6b18d0",  
    5|    "hostId":"shard-00-00.mongodb.net:27017",  
    6|    "links":[],  
    7|    "measurements":[  
    8|       {  
    9|          "dataPoints":[  
    10|             {  
    11|                "timestamp":"2021-04-09T18:07:45Z",  
    12|                "value":0.0  
    13|             }  
    14|          ],  
    15|          "name": "DISK_PARTITION_IOPS_READ",  
    16|          "units":"SCALAR_PER_SECOND"  
    17|       }  
    18|    ],  
    19|    "partitionName":"xvdb",  
    20|    "processId":"shard-00-00.mongodb.net:27017",  
    21|    "start":"2021-04-09T18:07:45Z"  
    22| }  
  
What is MongoDB Atlas? →

