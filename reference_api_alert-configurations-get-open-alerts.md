Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Open Alerts for Alert Configuration

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Serverless Measurements
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

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/alertConfigs/{ALERT-CONFIG-ID}/alerts  
      
  
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
  
`{ALERT-CONFIG-ID}`

|

Required

|

Alert configuration identifier.  
  
### Request Query Parameters

This endpoint may use any of the HTTP request query parameters available to
all Atlas Administration API resources. These are all optional.

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
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response Elements

The response includes the `totalCount` of the open alerts and a `results`
array which lists all the alerts for the project. Alert details include:

## Note

Alert details vary. An alert may only include a subset of these elements.

Name

|

Type

|

Description  
  
||  
  
`id`

|

string

|

Unique identifier for the alert.  
  
`groupId`

|

string

|

ID of the project that this alert was opened for.  
  
`alertConfigId`

|

string

|

ID of the alert configuration that triggered this alert.  
  
`eventTypeName`

|

string

|

Human-readable label that indicates the type of event.

## Important

The complete list of event type values changes frequently.

 **Atlas App Services**

  * `AUTH_LOGIN_FAIL`

Number of failed client login requests per second meets the

specified threshold.

  * `ENDPOINTS_COMPUTE_MS`

HTTPS endpoints

compute time per

second meets the specified threshold.

  * `ENDPOINTS_EGRESS_BYTES`

HTTPS endpoints

data egress bytes per

second meets the specified threshold.

  * `ENDPOINTS_FAILED_REQUESTS`

Number of HTTPS endpoints requests that fail per second meets the

specified threshold.

  * `ENDPOINTS_RESPONSE_MS`

95th percentile of duration in milliseconds for HTTPS endpoint

requests meets the specified threshold.

  * `GRAPHQL_COMPUTE_MS`

GraphQL compute time per second meets the specified

threshold.

  * `GRAPHQL_EGRESS_BYTES`

GraphQL data egress bytes

per second meets the specified threshold.

  * `GRAPHQL_FAILED_REQUESTS`

Number of GraphQL requests that fail per second meets the

specified threshold.

  * `GRAPHQL_RESPONSE_MS`

95th percentile of duration in milliseconds for GraphQL requests

meets the specified threshold.

  * `OVERALL_COMPUTE_MS`

Overall compute time per second meets the specified

threshold.

  * `OVERALL_EGRESS_BYTES`

Overall data egress bytes

per second meets the specified threshold.

  * `OVERALL_FAILED_REQUESTS`

Number of requests that fail per second meets the specified

threshold.

  * `SDKFNS_FAILED_REQUESTS`

Number of SDK Function requests that fail per second meets the

specified threshold.

  * `SDK_FNS_RESPONSE_MS`

95th percentile of duration in milliseconds for SDK function

requests meets the specified threshold.

  * `SDK_FUNCTIONS_COMPUTE_MS`

SDK Functions compute time per second meets the specified

threshold.

  * `SDK_FUNCTIONS_EGRESS_BYTES`

SDK Functions data egress

bytes per second meets the specified threshold.

  * `SDK_MQL_COMPUTE_MS`

SDK MQL compute time per second meets the specified

threshold.

  * `SDK_MQL_EGRESS_BYTES`

SDK MQL data egress bytes

per second meets the specified threshold.

  * `SDK_MQL_RESPONSE_MS`

95th percentile of duration in milliseconds for MQL requests meets

the specified threshold.

  * `SYNC_CURRENT_OPLOG_LAG_MS_SUM`

Approximate amount of time that the

Atlas Device Sync is behind

the MongoDB oplog meets the specified threshold.

  * `SYNC_EGRESS_BYTES`

Atlas Device Sync

data egress bytes per

second meets the specified threshold.

  * `SYNC_NUM_UNSYNCABLE_DOCS_LIMIT`

Percentage of App Services unsyncable documents meets

the specified threshold.

  * `TRIGGERS_COMPUTE_MS`

Triggers compute time per second has meets the

specified threshold.

  * `TRIGGERS_CURRENT_OPLOG_LAG_MS_SUM`

Approximate amount of time that the App Services triggers is

behind the MongoDB oplog meets the specified threshold.

  * `TRIGGERS_EGRESS_BYTES`

Triggers data egress bytes

per second meets the specified threshold.

  * `TRIGGERS_FAILED_REQUESTS`

Number of Triggers requests that fail per second meets the

specified threshold.

  * `TRIGGERS_RESPONSE_MS`

95th percentile of duration in milliseconds for triggers meets

the specified threshold.

 **Backup**

  * `CPS_SNAPSHOT_BEHIND`

Snapshot schedule fell behind

 **Billing**

  * `CREDIT_CARD_ABOUT_TO_EXPIRE`

Credit card is about to expire

  * `PENDING_INVOICE_OVER_THRESHOLD`

Monthly pending invoice ($) total is...

  * `DAILY_BILL_OVER_THRESHOLD`:

Daily amount billed ($) is...

 **Encryption Key**

  * `AWS_ENCRYPTION_KEY_NEEDS_ROTATION`

AWS encryption key elapsed time since last rotation is...

  * `AZURE_ENCRYPTION_KEY_NEEDS_ROTATION`

Azure encryption key elapsed time since last rotation is...

  * `GCP_ENCRYPTION_KEY_NEEDS_ROTATION`

GCP encryption key elapsed time since last rotation is...

 **Host**

  * `HOST_DOWN`

Host is down

  * `OUTSIDE_METRIC_THRESHOLD`

Metric occurred outside of the metric threshold.

To learn more, see Review Database Deployment Metrics.

  * `HOST_MONGOT_CRASHING_OOM`

Search process (`mongot`) ran out of memory.

To learn more and troubleshoot the issue that triggered this

alert, see Atlas Search alerts.

  * `MONGOT_NOT_CRASHING_OOM`

Search process (`mongot`) has enough memory.

 **Project**

  * `USERS_WITHOUT_MULTI_FACTOR_AUTH`

Users do not have two-factor authentication enabled

 **Replica Set**

  * `NO_PRIMARY`

Replica set has no primary

  * `TOO_MANY_ELECTIONS`

Number of election events is...

  * `REPLICATION_OPLOG_WINDOW_RUNNING_OUT`

Replication Oplog Window is...

 **Serverless**

  * `OUTSIDE_SERVERLESS_METRIC_THRESHOLD`.

Serverless metric occurred outside of the metric threshold.

To learn more, see Review Serverless Metrics.

 **Sharded Cluster**

  * `CLUSTER_MONGOS_IS_MISSING`

Cluster is missing an active mongos

 **X.509**

  * `NDS_X509_USER_AUTHENTICATION_MANAGED_USER_CERTS_EXPIRATION_CHECK`

X.509 User Authentication, Client Certificates Expiration

Alert when days to expiration is...

  * `NDS_X509_USER_AUTHENTICATION_CUSTOMER_CA_EXPIRATION_CHECK`

X.509 User Authentication, Self-Managed CA Expiration Alert

when days to expiration is...

  
  
`typeName`

|

string

|

 _This field is deprecated and will be ignored._  
  
`status`

|

string

|

The current state of the alert. Possible values are:

  * `TRACKING`

The alert condition exists but has not persisted beyond the defined
notification delay. For details, see Request Query Parameters.

  * `OPEN`

  * `CLOSED`

  * `CANCELLED`

  
  
`acknowledgedUntil`

|

date

|

The date through which the alert has been acknowledged. Will not be present if
the alert has never been acknowledged.  
  
`acknowledgementComment`

|

string

|

The comment left by the user who acknowledged the alert. Will not be present
if the alert has never been acknowledged.  
  
`acknowledgingUsername`

|

string

|

The username of the user who acknowledged the alert. Will not be present if
the alert has never been acknowledged.  
  
`created`

|

date

|

When the alert was opened.  
  
`updated`

|

date

|

When the alert was last updated.  
  
`resolved`

|

date

|

When the alert was closed. Only present if the status is `CLOSED`.  
  
`lastNotified`

|

date

|

When the last notification was sent for this alert. Only present if
notifications have been sent.  
  
`hostnameAndPort`

|

string

|

The hostname and port of each host to which the alert applies. Only present
for alerts of type `HOST`, `HOST_METRIC`, and `REPLICA_SET`.  
  
`hostId`

|

string

|

ID of the host to which the metric pertains. Only present for alerts of type
`HOST`, `HOST_METRIC`, and `REPLICA_SET`.  
  
`replicaSetName`

|

string

|

Name of the replica set. Only present for alerts of type `HOST`,
`HOST_METRIC`, `BACKUP`, and `REPLICA_SET`.  
  
`metricName`

|

string

|

The name of the measurement whose value went outside the threshold. Only
present if `eventTypeName` is set to `OUTSIDE_METRIC_THRESHOLD` or
`OUTSIDE_SERVERLESS_METRIC_THRESHOLD`.

To learn more about the available metrics, see Host Metrics.

## Note

If you set `eventTypeName` to `OUTSIDE_SERVERLESS_METRIC_THRESHOLD`, you can
specify only metrics available for serverless. To learn more, see Serverless
Measurements.  
  
`currentValue`

|

object

|

The current value of the metric that triggered the alert. Only present for
alerts of type `HOST_METRIC`.  
  
`currentValue.number`

|

number

|

The value of the metric.  
  
`currentValue.units`

|

string

|

The units for the value. Depends on the type of metric. For example, a metric
that measures memory consumption would have a byte measurement, while a metric
that measures time would have a time unit. Possible values are:

  * `RAW`

  * `BITS`

  * `BYTES`

  * `KILOBITS`

  * `KILOBYTES`

  * `MEGABITS`

  * `MEGABYTES`

  * `GIGABITS`

  * `GIGABYTES`

  * `TERABYTES`

  * `PETABYTES`

  * `NANOSECONDS`

  * `MILLISECONDS`

  * `SECONDS`

  * `MINUTES`

  * `HOURS`

  * `MILLION_MINUTES`

  * `DAYS`

  * `RPU`

  * `THOUSAND_RPU`

  * `MILLION_RPU`

  * `WPU`

  * `THOUSAND_WPU`

  * `MILLION_WPU`

  
  
`clusterId`

|

string

|

The ID of the cluster to which this alert applies. Only present for alerts of
type `BACKUP`, `REPLICA_SET`, and `CLUSTER`.  
  
`clusterName`

|

string

|

The name the cluster to which this alert applies. Only present for alerts of
type `BACKUP`, `REPLICA_SET`, and `CLUSTER`.  
  
`sourceTypeName`

|

string

|

For alerts of the type `BACKUP`, the type of server being backed up. Possible
values are:

  * `REPLICA_SET`

  * `SHARDED_CLUSTER`

  * `CONFIG_SERVER`

  
  
### Serverless Measurements

Metric Name

|

Description  
  
|  
  
`SERVERLESS_CONNECTIONS`

|

Number of active connections to the serverless instance meets the specified
average.  
  
`SERVERLESS_CONNECTIONS_PERCENT`

|

Number of open connections to the serverless instance exceeds the specified
percentage threshold.  
  
`SERVERLESS_DATA_SIZE_TOTAL`

|

Approximate size of all documents (and their paddings) meets the specified
threshold.  
  
`SERVERLESS_NETWORK_BYTES_IN`

|

Number of bytes sent _to_ MongoDB meets the specified threshold.  
  
`SERVERLESS_NETWORK_BYTES_OUT`

|

Number of bytes sent _from_ MongoDB meets the specified threshold.  
  
`SERVERLESS_NETWORK_NUM_REQUESTS`

|

Number of requests sent to MongoDB meets the specified average.  
  
`SERVERLESS_OPCOUNTER_CMD`

|

Rate of commands performed meets the specified threshold.  
  
`SERVERLESS_OPCOUNTER_DELETE`

|

Rate of deletes meets the specified threshold.  
  
`SERVERLESS_OPCOUNTER_GETMORE`

|

Rate of `getmore` operations to retrieve the next cursor batch meets the
specified threshold.  
  
`SERVERLESS_OPCOUNTER_INSERT`

|

Rate of inserts meets the specified threshold.  
  
`SERVERLESS_OPCOUNTER_QUERY`

|

Rate of queries meets the specified threshold.  
  
`SERVERLESS_OPCOUNTER_UPDATE`

|

Rate of updates meets the specified threshold.  
  
`SERVERLESS_TOTAL_READ_UNITS`

|

Total read units meet the specified threshold.  
  
`SERVERLESS_TOTAL_WRITE_UNITS`

|

Total write units meet the specified threshold.  
  
## Example Request

    
    
    curl -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/535683b3794d371327b/alertConfigs/533dc40ae4b00835ff81eaee/alerts"  
      
  
## Example Response

    
    
    {  
      
      "totalCount" : 2,  
      "results" : [ {  
        "id" : "53569159300495c7702ee3a3",  
        "groupId" : "535683b3794d371327b",  
        "eventTypeName" : "OUTSIDE_METRIC_THRESHOLD",  
        "status" : "OPEN",  
        "acknowledgedUntil" : "2016-09-01T14:00:00Z",  
        "created" : "2016-08-22T15:57:13.562Z",  
        "updated" : "2016-08-22T20:14:11.388Z",  
        "lastNotified" : "2016-08-22T15:57:24.126Z",  
        "metricName" : "ASSERT_REGULAR",  
        "currentValue" : {  
          "number" : 0.0,  
          "units" : "RAW"  
        },  
        "links" : [ ... ]  
      }, {  
        "id" : "5356ca0e300495c770333340",  
        "groupId" : "535683b3794d371327b",  
        "eventTypeName" : "OUTSIDE_METRIC_THRESHOLD",  
        "status" : "OPEN",  
        "created" : "2016-08-22T19:59:10.657Z",  
        "updated" : "2016-08-22T20:14:11.388Z",  
        "lastNotified" : "2016-08-22T20:14:19.313Z",  
        "metricName" : "ASSERT_REGULAR",  
        "currentValue" : {  
          "number" : 0.0,  
          "units" : "RAW"  
        },  
        "links" : [ ... ]  
      } ],  
      "links" : [ ... ]  
    }  
  
What is MongoDB Atlas? →

