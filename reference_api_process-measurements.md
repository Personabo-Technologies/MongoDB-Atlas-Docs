Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Measurements for a MongoDB Process

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

Get measurements for a specific Atlas MongoDB process. An Atlas MongoDB
process can be either a `mongod` or `mongos`.

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

    
    
    GET /groups/{GROUP-ID}/processes/{HOST}:{PORT}/measurements  
      
  
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
  
### Measurement Values

|  
  
|  
  
PROCESS_CPU_USER

MAX_PROCESS_CPU_USER

PROCESS_CPU_KERNEL

MAX_PROCESS_CPU_KERNEL

PROCESS_CPU_CHILDREN_USER

MAX_PROCESS_CPU_CHILDREN_USER

PROCESS_CPU_CHILDREN_KERNEL

MAX_PROCESS_CPU_CHILDREN_KERNEL

|

MongoDB CPU usage. For hosts with more than one CPU core, these values can
exceed 100%.  
  
PROCESS_NORMALIZED_CPU_USER

MAX_PROCESS_NORMALIZED_CPU_USER

PROCESS_NORMALIZED_CPU_KERNEL

MAX_PROCESS_NORMALIZED_CPU_KERNEL

PROCESS_NORMALIZED_CPU_CHILDREN_USER

MAX_PROCESS_NORMALIZED_CPU_CHILDREN_USER

PROCESS_NORMALIZED_CPU_CHILDREN_KERNEL

MAX_PROCESS_NORMALIZED_CPU_CHILDREN_KERNEL

|

MongoDB CPU usage scaled to a range of 0% to 100%. Atlas computes this value
by dividing by the number of CPU cores.  
  
ASSERT_REGULAR

ASSERT_WARNING

ASSERT_MSG

ASSERT_USER

|

Rate of asserts for a MongoDB process found in the `asserts` document that the
`serverStatus` command generates.  
  
BACKGROUND_FLUSH_AVG

|

Amount of data flushed in the background.  
  
CACHE_BYTES_READ_INTO

CACHE_BYTES_WRITTEN_FROM

CACHE_DIRTY_BYTES

CACHE_USED_BYTES

TICKETS_AVAILABLE_READS

TICKETS_AVAILABLE_WRITE

|

Amount of bytes in the WiredTiger storage engine cache and tickets found in
the `wiredTiger.cache` and `wiredTiger.concurrentTransactions` documents that
the `serverStatus` command generates.  
  
CONNECTIONS

|

Number of connections to a MongoDB process found in the `connections` document
that the `serverStatus` command generates.  
  
CURSORS_TOTAL_OPEN

CURSORS_TOTAL_TIMED_OUT

|

Number of cursors for a MongoDB process found in the `metrics.cursor` document
that the `serverStatus` command generates.  
  
EXTRA_INFO_PAGE_FAULTS

GLOBAL_ACCESSES_NOT_IN_MEMORY

GLOBAL_PAGE_FAULT_EXCEPTIONS_THROWN

|

Numbers of **Memory Issues** and **Page Faults** for a MongoDB process.  
  
GLOBAL_LOCK_CURRENT_QUEUE_TOTAL

GLOBAL_LOCK_CURRENT_QUEUE_READERS

GLOBAL_LOCK_CURRENT_QUEUE_WRITERS

|

Number of operations waiting on locks for the MongoDB process that the
`serverStatus` command generates. Cloud Manager computes these values based on
the type of storage engine.  
  
INDEX_COUNTERS_BTREE_ACCESSES

INDEX_COUNTERS_BTREE_HITS

INDEX_COUNTERS_BTREE_MISSES

INDEX_COUNTERS_BTREE_MISS_RATIO

|

Number of index btree operations.  
  
JOURNALING_COMMITS_IN_WRITE_LOCK

JOURNALING_MB

JOURNALING_WRITE_DATA_FILES_MB

|

Number of journaling operations.  
  
MEMORY_RESIDENT

MEMORY_VIRTUAL

MEMORY_MAPPED

COMPUTED_MEMORY

|

Amount of memory for a MongoDB process found in the `mem` document that the
`serverStatus` command collects.  
  
NETWORK_BYTES_IN

NETWORK_BYTES_OUT

NETWORK_NUM_REQUESTS

|

Amount of throughput for MongoDB process found in the `network` document that
the `serverStatus` command collects.  
  
OPLOG_REPLICATION_LAG_TIME

OPLOG_SLAVE_LAG_MASTER_TIME

OPLOG_MASTER_TIME

OPLOG_MASTER_LAG_TIME_DIFF

OPLOG_RATE_GB_PER_HOUR

|

Durations and throughput of the MongoDB process' oplog. The
`OPLOG_SLAVE_LAG_MASTER_TIME` metric is deprecated. Use the
`OPLOG_REPLICATION_LAG_TIME` metric instead. It returns decimal values
(seconds and milliseconds). For example, the value 2.75 means 2 seconds and
750 milliseconds.  
  
DB_STORAGE_TOTAL

DB_DATA_SIZE_TOTAL

|

Measures the database's on-disk storage space, as collected from the MongoDB
`dbStats` command.  
  
OPCOUNTER_CMD

OPCOUNTER_QUERY

OPCOUNTER_UPDATE

OPCOUNTER_DELETE

OPCOUNTER_GETMORE

OPCOUNTER_INSERT

|

Rate of database operations on a MongoDB process since the process last
started found in the `opcounters` document that the `serverStatus` command
collects.  
  
OPCOUNTER_REPL_CMD

OPCOUNTER_REPL_UPDATE

OPCOUNTER_REPL_DELETE

OPCOUNTER_REPL_INSERT

|

Rate of database operations on MongoDB secondaries found in the
`opcountersRepl` document that the `serverStatus` command collects.  
  
DOCUMENT_METRICS_RETURNED

DOCUMENT_METRICS_INSERTED

DOCUMENT_METRICS_UPDATED

DOCUMENT_METRICS_DELETED

|

Average rate of documents returned, inserted, updated, or deleted per second
during a selected time period.  
  
OPERATIONS_SCAN_AND_ORDER

|

Average rate for operations per second during a selected time period that
perform a sort but cannot perform the sort using an index.  
  
OP_EXECUTION_TIME_READS

OP_EXECUTION_TIME_WRITES

OP_EXECUTION_TIME_COMMANDS

|

Average execution time in milliseconds per read, write, or command operation
during a selected time period.  
  
RESTARTS_IN_LAST_HOUR

|

Number of times the host restarted within the previous hour.  
  
QUERY_EXECUTOR_SCANNED

|

Average rate per second to scan index items during queries and query-plan
evaluations found in the value of **totalKeysExamined** from the `explain`
command.  
  
QUERY_EXECUTOR_SCANNED_OBJECTS

|

Average rate of documents scanned per second during queries and query-plan
evaluations found in the value of **totalDocsExamined** from the `explain`
command.  
  
QUERY_TARGETING_SCANNED_PER_RETURNED

|

Ratio of the number of index items scanned to the number of documents
returned.  
  
QUERY_TARGETING_SCANNED_OBJECTS_PER_RETURNED

|

Ratio of the number of documents scanned to the number of documents returned.  
  
SYSTEM_CPU_USER

MAX_SYSTEM_CPU_USER

SYSTEM_CPU_KERNEL

MAX_SYSTEM_CPU_KERNEL

SYSTEM_CPU_NICE

MAX_SYSTEM_CPU_KERNEL

SYSTEM_CPU_IOWAIT

MAX_SYSTEM_CPU_IOWAIT

SYSTEM_CPU_IRQ

MAX_SYSTEM_CPU_IRQ

SYSTEM_CPU_SOFTIRQ

MAX_SYSTEM_CPU_SOFTIRQ

SYSTEM_CPU_GUEST

MAX_SYSTEM_CPU_GUEST

SYSTEM_CPU_STEAL

MAX_SYSTEM_CPU_STEAL

|

CPU usage of processes on the host. For hosts with more than one CPU core,
this value can exceed 100%.  
  
SYSTEM_NORMALIZED_CPU_USER

MAX_SYSTEM_NORMALIZED_CPU_USER

SYSTEM_NORMALIZED_CPU_KERNEL

MAX_SYSTEM_NORMALIZED_CPU_KERNEL

SYSTEM_NORMALIZED_CPU_NICE

MAX_SYSTEM_NORMALIZED_CPU_NICE

SYSTEM_NORMALIZED_CPU_IOWAIT

MAX_SYSTEM_NORMALIZED_CPU_IOWAIT

SYSTEM_NORMALIZED_CPU_IRQ

MAX_SYSTEM_NORMALIZED_CPU_IRQ

SYSTEM_NORMALIZED_CPU_SOFTIRQ

MAX_SYSTEM_NORMALIZED_CPU_SOFTIRQ

SYSTEM_NORMALIZED_CPU_GUEST

MAX_SYSTEM_NORMALIZED_CPU_GUEST

SYSTEM_NORMALIZED_CPU_STEAL

MAX_SYSTEM_NORMALIZED_CPU_STEAL

|

CPU usage of processes on the host scaled to a range of 0 to 100% by dividing
by the number of CPU cores.  
  
SYSTEM_MEMORY_AVAILABLE

MAX_SYSTEM_MEMORY_AVAILABLE

SYSTEM_MEMORY_FREE

MAX_SYSTEM_MEMORY_FREE

SYSTEM_MEMORY_USED

MAX_SYSTEM_MEMORY_USED

|

Physical memory usage, in bytes, that the host uses.  
  
SYSTEM_NETWORK_IN

MAX_SYSTEM_NETWORK_IN

SYSTEM_NETWORK_OUT

MAX_SYSTEM_NETWORK_OUT

|

Average rate of physical bytes per second that the **eth0** network interface
received and transmitted.  
  
SWAP_USAGE_USED

MAX_SWAP_USAGE_USED

SWAP_USAGE_FREE

MAX_SWAP_USAGE_FREE

|

Total amount of memory that swap uses.  
  
FTS_MEMORY_RESIDENT

FTS_MEMORY_VIRTUAL

FTS_MEMORY_MAPPED

|

Memory usage, in bytes, that Atlas Search processes use.  
  
FTS_DISK_UTILIZATION

|

Disk space, in bytes, that Atlas Search indexes use.  
  
FTS_PROCESS_CPU_USER

FTS_PROCESS_CPU_KERNEL

FTS_PROCESS_NORMALIZED_CPU_USER

FTS_PROCESS_NORMALIZED_CPU_KERNEL

|

Percentage of CPU that Atlas Search processes use.  
  
## Example Request

The following example request sets a **granularity** and **period** of one
minute. Replace the information in brackets `{}` with your own Atlas
information to execute this example request:

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Content-Type: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/processes/{HOST}:{PORT}/measurements?granularity=PT1M&period=PT1M&pretty=true"  
  
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
    2|   "end" : "2021-04-09T20:31:14Z",  
    3|   "granularity" : "PT1M",  
    4|   "groupId" : "{GROUP-ID}",  
    5|   "hostId" : "shard-00-00.mongodb.net:27017",  
    6|   "links":[],  
    7|   "measurements" : [  
    8|     {  
    9|       "dataPoints": [  
    10|         {  
    11|           "timestamp": "2021-04-09T10:06:15Z",  
    12|           "value": 0.0  
    13|         }  
    14|       ],  
    15|       "name": "QUERY_EXECUTOR_SCANNED",  
    16|       "units": "SCALAR_PER_SECOND"  
    17|     },{  
    18|       "dataPoints": [  
    19|         {  
    20|           "timestamp": "2021-04-09T10:06:15Z",  
    21|           "value": 6.866666666666666  
    22|         }  
    23|       ],  
    24|       "name": "QUERY_EXECUTOR_SCANNED_OBJECTS",  
    25|       "units": "SCALAR_PER_SECOND"  
    26|     },{  
    27|       "dataPoints": [  
    28|         {  
    29|           "timestamp": "2021-04-09T10:06:15Z",  
    30|           "value": 0.0  
    31|         }  
    32|       ],  
    33|       "name": "QUERY_TARGETING_SCANNED_PER_RETURNED",  
    34|       "units": "SCALAR"  
    35|     },{  
    36|       "dataPoints": [  
    37|         {  
    38|           "timestamp": "2021-04-09T10:06:15Z",  
    39|           "value": 1.0147783251231526  
    40|         }  
    41|       ],  
    42|       "name": "QUERY_TARGETING_SCANNED_OBJECTS_PER_RETURNED",  
    43|       "units": "SCALAR"  
    44|     }  
    45|   ],  
    46|   "processId" : "shard-00-00.mongodb.net:27017",  
    47|   "start" : "2021-04-09T20:30:45Z"  
    48| }  
  
What is MongoDB Atlas? →

