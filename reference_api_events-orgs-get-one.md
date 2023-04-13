Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Organization Event

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
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

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /orgs/{ORG-ID}/events/{EVENT-ID}  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`ORG-ID`

|

Required

|

The unique identifier for the organization whose events you want to retrieve.
Use the /orgs endpoint to retrieve all organizations to which the
authenticated user has access.  
  
`EVENT-ID`

|

Required

|

The unique identifier for the event which you want to retrieve.  
  
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
  
includeRaw

|

boolean

|

Optional

|

Flag that indicates whether to include the `raw` document in the output. The
`raw` document contains additional meta information about the event.

## Important

The values in the `raw` document are subject to change. Do not rely on `raw`
values for formal monitoring.

|

`false`  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

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
      "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5b478b3afc4625789ce616a3/events/5b48f4d2d7e33a1c0c60597e"  
  
## Example Response

    
    
    {  
      
      "created": "2018-06-19T15:06:15Z",  
      "eventTypeName": "JOINED_ORG",  
      "id": "5b48f4d2d7e33a1c0c60597e",  
      "isGlobalAdmin": false,  
      "links": [  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5b478b3afc4625789ce616a3",  
          "rel": "http://mms.mongodb.com/org"  
        },  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/6b610e1087d9d66b272f0c86",  
          "rel": "http://mms.mongodb.com/user"  
        },  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/5b478b3afc4625789ce616a3/events/5b48f4d2d7e33a1c0c60597e",  
          "rel": "self"  
        }  
      ],  
      "orgId": "5b478b3afc4625789ce616a3",  
      "remoteAddress": "198.51.100.64",  
      "targetUsername": "j.doe@example.com",  
      "userId": "6b610e1087d9d66b272f0c86",  
      "username": "j.doe@example.com"  
    }  
  
What is MongoDB Atlas? →

