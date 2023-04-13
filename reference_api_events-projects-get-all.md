Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Project Events

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Event Type Values
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/events  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required

|

The unique identifier for the project in which the event associated to `EVENT-
ID` occurred. Use the /groups endpoint to retrieve all projects to which the
authenticated user has access.  
  
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
  
clusterNames

|

string

|

Optional

|

Cluster on which the events occurred. To return events from multiple clusters,
specify multiple `clusterNames` query parameters. For example:

    
    
    | <Request URL>?clusterNames=Cluster1&clusterNames=Cluster2  
      
  
eventType

|

string

|

Optional

|

Human-readable label that indicates the type of event.

Atlas accepts:

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

|  
  
minDate

|

date

|

Optional

|

Earliest Timestamp in ISO 8601 date and time format in UTC from when Atlas
should return events.

|  
  
maxDate

|

date

|

Optional

|

Latest Timestamp in ISO 8601 date and time format in UTC from when Atlas
should return events.

|  
  
includeRaw

|

boolean

|

Optional

|

Flag that specifies whether to include the `raw` document in the output. The
`raw` document contains additional meta information about the event.

## Important

The values in the `raw` document are subject to change. Do not rely on `raw`
values for formal monitoring.

|

`false`  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

### Response Document

The response JSON document includes an array of **result** objects, an array
of **link** objects and a count of the total number of **result** objects
retrieved.

Name

|

Type

|

Description  
  
||  
  
results

|

array of objects

|

One object for each item detailed in the results Embedded Document section.  
  
links

|

array of objects

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
totalCount

|

integer

|

Count of the total number of items in the result set. It may be greater than
the number of objects in the **results** array if the entire result set is
paginated.  
  
### results Embedded Document

Name

|

Type

|

Description  
  
||  
  
`alertId`

|

string

|

Unique identifier for the alert associated to the event.  
  
`alertConfigId`

|

string

|

Unique identifier for the alert configuration associated to the `alertId`.  
  
`apiKeyId`

|

string

|

Unique identifier for the API Key that triggered the event. If this field is
present in the response, Atlas does not return the `userId` field.  
  
`collection`

|

string

|

Name of the collection on which the event occurred. This field can be present
when the `eventTypeName` is either `DATA_EXPLORER` or `DATA_EXPLORER_CRUD`.  
  
`created`

|

date

|

ISO 8601-formatted UTC date when the event occurred.  
  
`currentValue`

|

document

|

Describes the value of the `metricName` at the time of the event.  
  
`currentValue.number`

|

int

|

The value of the `metricName` at the time of the event.  
  
`currentValue.units`

|

string

|

The unit of measurement of the `currentValue.number`.

Possible values are:

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

  
  
`database`

|

string

|

Name of the database on which the event occurred. This field can be present
when the `eventTypeName` is either `DATA_EXPLORER` or `DATA_EXPLORER_CRUD`.  
  
`eventTypeName`

|

string

|

Human-readable label that indicates the type of event.  
  
`groupId`

|

string

|

The unique identifier for the project in which the event occurred.  
  
`hostname`

|

string

|

The hostname of the Atlas host machine associated to the event.  
  
`id`

|

string

|

The unique identifier for the event.  
  
`invoiceId`

|

string

|

The unique identifier of the invoice associated to the event.  
  
`isGlobalAdmin`

|

boolean

|

Indicates whether the user who triggered the event is a MongoDB employee.  
  
`links`

|

array

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
`metricName`

|

string

|

The name of the metric associated to the `alertId`.  
  
`opType`

|

string

|

Type of operation that occurred. This field is present when the
`eventTypeName` is either `DATA_EXPLORER` or `DATA_EXPLORER_CRUD`.  
  
`orgId`

|

string

|

The unique identifier for the organization in which the event occurred.  
  
`paymentId`

|

string

|

The unique identifier of the invoice payment associated to the event.  
  
`port`

|

int

|

The port on which the `mongod` or `mongos` listens.  
  
`publicKey`

|

string

|

Public key associated with the API Key that triggered the event. If this field
is present in the response, Atlas does not return the `username` field.  
  
`raw`

|

document

|

Additional meta information about the event. This field only appears when the
`includeRaw` query parameter is `true`.

## Important

The values in the `raw` document are subject to change. Do not rely on `raw`
values for formal monitoring.  
  
`remoteAddress`

|

string

|

IP address of the `userId` Atlas user who triggered the event.  
  
`replicaSetName`

|

string

|

The name of the replica set associated to the event.  
  
`shardName`

|

string

|

The name of the shard associated to the event.  
  
`targetPublicKey`

|

string

|

The public key of the API Key targeted by the event.  
  
`targetUsername`

|

string

|

The username for the Atlas user targeted by the event.  
  
`teamId`

|

string

|

The unique identifier for the Atlas team associated to the event.  
  
`userId`

|

string

|

The unique identifier for the Atlas user who triggered the event. If this
field is present in the response, Atlas does not return the `apiKeyId` field.  
  
`username`

|

string

|

The username for the Atlas user who triggered the event. If this field is
present in the response, Atlas does not return the `publicKey` field.  
  
`whitelistEntry`

|

string

|

The white list entry of the API Key targeted by the event.  
  
### Event Type Values

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

## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
      --header "Content-Type: application/json" \  
      "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b478b3afc4625789ce616a3/events"  
  
## Example Response

    
    
    {  
      
        "links": [  
            {  
                "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b478b3afc4625789ce616a3/events?pageNum=1&itemsPerPage=100",  
                "rel": "self"  
            },  
            {  
                "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b478b3afc4625789ce616a3/events?itemsPerPage=100&pageNum=2",  
                "rel": "next"  
            }  
        ],  
        "results": [  
            {  
                "created": "2018-06-04T19:19:00Z",  
                "eventTypeName": "HOST_NOW_PRIMARY",  
                "groupId": "5b478b3afc4625789ce616a3",  
                "hostname": "example-shard-0-abc0p.mongodb.net",  
                "id": "5b478c2562c892f9824cd990",  
                "links": [  
                    {  
                        "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b478b3afc4625789ce616a3/events/5b478c2562c892f9824cd990",  
                        "rel": "self"  
                    }  
                ],  
                "port": 27017,  
                "replicaSetName": "example-shard-0"  
            },  
            {  
                "created": "2018-06-04T19:16:19Z",  
                "eventTypeName": "HOST_RESTARTED",  
                "groupId": "5b478b3afc4625789ce616a3",  
                "hostname": "example-shard-0-abc0p.mongodb.net",  
                "id": "6b610e4f80eef5366613e4df",  
                "links": [  
                    {  
                        "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b478b3afc4625789ce616a3/events/6b610e4f80eef5366613e4df",  
                        "rel": "self"  
                    }  
                ],  
                "port": 27017,  
                "replicaSetName": "example-shard-0"  
            }  
        ],  
        "totalCount": 2  
    }  
  
What is MongoDB Atlas? →

