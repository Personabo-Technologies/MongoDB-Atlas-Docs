Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Alert Configurations for a Group

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

    
    
    GET /groups/{GROUP-ID}/alertConfigs  
      
  
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

The response includes the `totalCount` of the alert configurations and a
`results` array which lists all alert configurations for the group. Each alert
configuration includes:

## Note

Alert configurations vary. An alert configuration may only include a subset of
these elements.

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

Unique identifier of the alert configuration.  
  
`groupId`

|

string

|

Unique identifier of the project that owns this alert configuration.  
  
`eventTypeName`

|

string

|

Human-readable label that indicates the type of event.

Accepted values are:

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

  * `CPS_SNAPSHOT_SUCCESSFUL`

Snapshot taken successfully

  * `CPS_SNAPSHOT_FALLBACK_SUCCESSFUL`

Fallback snapshot taken

  * `CPS_SNAPSHOT_FALLBACK_FAILED`

Fallback snapshot failed

  * `CPS_SNAPSHOT_BEHIND`

Snapshot schedule fell behind

  * `CPS_RESTORE_FAILED`

Backup restore failed

  * `CPS_RESTORE_SUCCESSFUL`

Backup restore succeeded

  * `CPS_SNAPSHOT_DOWNLOAD_REQUEST_FAILED`

Snapshot download request failed

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

  * `PRIMARY_ELECTED`

Replica set elected a new primary

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

 **User**

  * `USER_ROLES_CHANGED_AUDIT`

User had their role changed

  * `JOINED_GROUP`

User joined the project

  * `REMOVED_FROM_GROUP`

User left the project

 **X.509**

  * `NDS_X509_USER_AUTHENTICATION_MANAGED_USER_CERTS_EXPIRATION_CHECK`

X.509 User Authentication, Client Certificates Expiration

Alert when days to expiration is...

  * `NDS_X509_USER_AUTHENTICATION_CUSTOMER_CA_EXPIRATION_CHECK`

X.509 User Authentication, Self-Managed CA Expiration Alert

when days to expiration is...

  
  
`created`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when this alert
configuration was created.  
  
`updated`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when this alert
configuration was last updated.  
  
`enabled`

|

boolean

|

If set to `true`, the alert configuration is enabled.

If `enabled` is not specified in a `POST` command, it defaults to `false`.  
  
`matchers`

|

object array

|

Rules to apply when matching an object against this alert configuration. Only
entities that match _all_ these rules are checked for an alert condition.

You can filter using the `matchers` array only when the `eventTypeName`
specifies an event for a host, replica set, or sharded cluster.  
  
`matchers`

`.fieldName`

|

string

|

Name of the field in the target object to match on.

  * Host alerts support these fields:

    * `TYPE_NAME`

    * `HOSTNAME`

    * `PORT`

    * `HOSTNAME_AND_PORT`

    * `REPLICA_SET_NAME`

  * Replica set alerts support these fields:

    * `REPLICA_SET_NAME`

    * `SHARD_NAME`

    * `CLUSTER_NAME`

  * Sharded cluster alerts support these fields:

    * `CLUSTER_NAME`

    * `SHARD_NAME`

All other types of alerts do not support matchers.  
  
`matchers`

`.operator`

|

string

|

Operator to test the field's value. Accepted values are:

  * `EQUALS`

  * `NOT_EQUALS`

  * `CONTAINS`

  * `NOT_CONTAINS`

  * `STARTS_WITH`

  * `ENDS_WITH`

  * `REGEX`

  
  
`matchers`

`.value`

|

string

|

Value to test with the specified operator.

If `"matchers.fieldName" : "TYPE_NAME"`, you can match on the following
values:

  * `PRIMARY`

  * `SECONDARY`

  * `STANDALONE`

  * `CONFIG`

  * `MONGOS`

  
  
`metricThreshold`

|

object

|

Threshold that causes an alert to be triggered. Populated if `eventTypeName`
is set to `OUTSIDE_METRIC_THRESHOLD` or `OUTSIDE_SERVERLESS_METRIC_THRESHOLD`.  
  
`metricThreshold`

`.metricName`

|

string

|

Name of the metric against which Atlas checks the configured
`metricThreshold.threshold`.

To learn more about the available metrics, see Host Metrics.

## Note

If you set `eventTypeName` to `OUTSIDE_SERVERLESS_METRIC_THRESHOLD`, you can
specify only metrics available for serverless. To learn more, see Serverless
Measurements.  
  
`metricThreshold`

`.operator`

|

string

|

Operator to apply when checking the current metric value against the threshold
value. Accepted values are:

  * `GREATER_THAN`

  * `LESS_THAN`

  
  
`metricThreshold`

`.threshold`

|

integer

|

Threshold value outside of which an alert will be triggered.  
  
`metricThreshold`

`.units`

|

string

|

Units for the threshold value. Depends on the type of metric.

## Example

A metric that measures memory consumption would have a byte measurement, while
a metric that measures time would have a time unit.

Accepted values are:

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

  
  
`metricThreshold`

`.mode`

|

string

|

`AVERAGE`. Atlas computes the current metric value as an average.  
  
`notifications`

|

object array

|

Notifications to send when an alert condition is detected.  
  
`notifications`

`.typeName`

|

string

|

Type of alert notification. Accepted values are:

  * `DATADOG`

  * `EMAIL`

  * `FLOWDOCK`

  * `GROUP` (Project)

  * `MICROSOFT_TEAMS`

  * `OPS_GENIE`

  * `ORG`

  * `PAGER_DUTY`

  * `SLACK`

  * `SMS`

  * `TEAM`

  * `USER`

  * `VICTOR_OPS`

  * `WEBHOOK`

  
  
`notifications`

`.intervalMin`

|

integer

|

Number of minutes to wait between successive notifications for unacknowledged
alerts that are not resolved.

## Note

PagerDuty, VictorOps, and OpsGenie notifications don't return this element.
You must configure and manage the notification interval within each external
service.  
  
`notifications`

`.delayMin`

|

integer

|

Number of minutes to wait after an alert condition is detected before sending
out the first notification.  
  
`notifications`

`.emailEnabled`

|

boolean

|

Flag indicating if email notifications should be sent. Returned with `ORG`,
`GROUP`, and `USER` notifications types.  
  
`notifications`

`.smsEnabled`

|

boolean

|

Flag indicating if text message notifications should be sent. Returned with
`ORG`, `GROUP`, and `USER` notifications types.  
  
`notifications`

`.username`

|

string

|

Name of the Atlas user to which to send notifications. Only a user in the
project that owns the alert configuration is allowed here. Returned with the
`USER` notifications type.  
  
`notifications`

`.roles`

|

array of strings

|

One or more project roles that receive the configured alert. Accepted values
include:

  * `GROUP_CLUSTER_MANAGER`

  * `GROUP_DATA_ACCESS_ADMIN`

  * `GROUP_DATA_ACCESS_READ_ONLY`

  * `GROUP_DATA_ACCESS_READ_WRITE`

  * `GROUP_OWNER`

  * `GROUP_READ_ONLY`

  
  
`notifications`

`.teamId`

|

string

|

Unique identifier of a team.  
  
`notifications`

`.emailAddress`

|

string

|

Email address to which alert notifications are sent. Returned with the `EMAIL`
notifications type.  
  
`notifications`

`.mobileNumber`

|

string

|

Mobile number to which alert notifications are sent. Returned with the `SMS`
notifications type.  
  
`notifications`

`.channelName`

|

string

|

Slack channel name. Returned with the `SLACK` notifications type.  
  
`notifications`

`.apiToken`

|

string

|

Slack API token or Bot token. Returned with the `SLACK` notifications type. If
the token later becomes invalid, Atlas sends an email to the project owner and
eventually removes the token.  
  
`notifications`

`.orgName`

|

string

|

Flowdock organization name in lower-case letters. This is the name that
appears after `www.flowdock.com/app/` in the URL string. Returned with the
`FLOWDOCK` notifications type.  
  
`notifications`

`.flowName`

|

string

|

Flowdock flow name in lower-case letters. The flow name appears after the
organization name in the URL string:

`www.flowdock.com/app/<organization-name>/<flow-name>`.

Returned with the `FLOWDOCK` notifications type.  
  
`notifications`

`.flowdockApiToken`

|

string

|

Flowdock personal API token. Returned with the `FLOWDOCK` notifications type.
If the token later becomes invalid, Atlas sends an email to the project owner
and eventually removes the token.  
  
`notifications`

`.serviceKey`

|

string

|

PagerDuty service key. Returned with the `PAGER_DUTY` notifications type. If
the key later becomes invalid, Atlas sends an email to the project owner and
eventually removes the key.  
  
`notifications`

`.victorOpsApiKey`

|

string

|

VictorOps API key. Returned with the `VICTOR_OPS` notifications type. If the
key later becomes invalid, Atlas sends an email to the project owner and
eventually removes the key.  
  
`notifications`

`.victorOpsRoutingKey`

|

string

|

VictorOps routing key. Returned with the `VICTOR_OPS` notifications type. If
the key later becomes invalid, Atlas sends an email to the project owner and
eventually removes the key.  
  
`notifications`

`.opsGenieApiKey`

|

string

|

Opsgenie API Key. Returned with the `OPS_GENIE` notifications type. If the key
later becomes invalid, Atlas sends an email to the project owner and
eventually removes the token.  
  
`notifications`

`.opsGenieRegion`

|

string

|

Region that indicates which API URL to use. Accepted regions are:

  * `US`

  * `EU`

The default Opsgenie region is `US`.  
  
`notifications`

`.datadogApiKey`

|

string

|

Datadog API Key. Found in the Datadog dashboard. Populated for the `DATADOG`
notifications type.  
  
`notifications`

`.datadogRegion`

|

string

|

Region that indicates the API URL to use.

Atlas supports the following Datadog regions in the Atlas Administration API:

|

Atlas Administration API region

|

Corresponding Datadog region  
  
|  
  
`US`

|

`US1`  
  
`US3`

|

`US3`  
  
`US5`

|

`US5`  
  
`EU`

|

`EU1`  
  
Datadog uses `US1` (`US` in the Atlas Administration API) by default.

To learn more about Datadog's regions, see Datadog Sites.  
  
`notifications`

`.webhookSecret`

|

string

|

Authentication secret for a webhook-based alert. Returned with the `WEBHOOK`
notifications type.  
  
`notifications`

`.webhookUrl`

|

string

|

Target URL for a webhook-based alert. Returned with the `WEBHOOK`
notifications type.  
  
`notifications`

`.microsoftTeamsWebhookUrl`

|

string

|

Microsoft Teams channel incoming webhook URL. Returned with the
`MICROSOFT_TEAMS` notifications type.  
  
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

    
    
    curl -X GET -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/535683b3794d371327b/alertConfigs"  
      
  
## Example Response

    
    
    {  
      
      "results": [ {  
        "id" : "533dc40ae4b00835ff81eaee",  
        "groupId" : "535683b3794d371327b",  
        "eventTypeName" : "OUTSIDE_METRIC_THRESHOLD",  
        "created" : "2016-08-23T20:26:50Z",  
        "updated" : "2016-08-23T20:26:50Z",  
        "enabled" : true,  
        "matchers" : [ {  
          "field" : "HOSTNAME_AND_PORT",  
          "operator" : "EQUALS",  
          "value" : "mongo.example.com:27017"  
        } ],  
        "notifications" : [ {  
          "typeName" : "SMS",  
          "intervalMin" : 5,  
          "delayMin" : 0,  
          "mobileNumber" : "2343454567"  
        } ],  
        "metricThreshold" : {  
          "metricName" : "ASSERT_REGULAR",  
          "operator" : "LESS_THAN",  
          "threshold" : 99.0,  
          "units" : "RAW",  
          "mode" : "AVERAGE"  
        },  
        "links" : [ ... ]  
      }, ... ],  
      "totalCount": 3,  
      "links" : [ ... ]  
    }  
  
What is MongoDB Atlas? →

