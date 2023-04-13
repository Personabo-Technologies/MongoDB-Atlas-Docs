Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update One Alert Configuration

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

## Syntax

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    PUT /groups/{GROUP-ID}/alertConfigs/{ALERT-CONFIG-ID}  
      
  
## Note

To enable or disable the alert configuration, see Enable/Disable Alert
Configuration.

### Request Path Parameters

Parameter

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

Unique identifier for the Project.  
  
`ALERT-CONFIG-ID`

|

string

|

Required

|

Unique identifier for the alert configuration.  
  
### Request Query Parameters

This endpoint might use any of the HTTP request query parameters available to
all Atlas Administration API resources. All of these are optional.

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
  
### Request Body Parameters

Alert configurations depend why you want Atlas to raise an alert. Alerts can
be triggered if either:

  * a particular condition is met or

  * a particular metric exceeded a particular value.

To simplify the differences between condition and metrics, click one of the
following tabs:

Condition

Metrics

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
enabled

|

boolean

|

Optional

|

Flag that indicates if this alert configuration is enabled or disabled.  
  
eventTypeName

|

string

|

Required

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

  
  
|

|

|  
  
|||  
  
matchers

|

array of objects

|

Required

|

Rules to apply when matching an object against this alert configuration. Only
entities that match _all_ these rules are checked for an alert condition.

Atlas limits filtering alerts using **matchers** when the **eventTypeName**
specifies an event for the following:

  * a host,

  * a replica set, or

  * a sharded cluster.

To add one or more **matchers** , see Filter Results.  
  
notifications

|

array of objects

|

Required

|

One or more targets for Atlas to send notifications when an alert condition is
detected. You can configure any number of notifications for each alert
condition.

To add one or more **notifications** , see Set Notifications.  
  
Condition

Metrics

|

|

|  
  
|||  
  
threshold

|

object

|

Conditional

|

Threshold that triggers an alert. Don't include if **"eventTypeName" :
"OUTSIDE_METRIC_THRESHOLD"**.

To add one **threshold** , see Trigger Alerts.  
  
#### Trigger Alerts

Condition

Metrics

|

|

|  
  
|||  
  
threshold

.operator

|

string

|

Required

|

Comparison operator to apply when checking the current condition against the
**threshold.threshold** value. Atlas accepts the following values:

  * `GREATER_THAN`

  * `LESS_THAN`

  
  
threshold

.threshold

|

integer

|

Required

|

Value that, when exceeded, Atlas triggers an alert.  
  
threshold.units

|

string

|

Required

|

Units of capacity or time that define the scope of the
**threshold.threshold**.  
  
#### Filter Results

|

|

|  
  
|||  
  
matchers

.[n].fieldName

|

string

|

Required

|

Name of the field in the target object that you wanted this configuration to
match. Atlas accepts the following values:

|

Host

|

Replica set

|

Sharded cluster  
  
||  
  
`TYPE_NAME`

`HOSTNAME`

`PORT`

`HOSTNAME_AND_PORT`

`REPLICA_SET_NAME`

|

`REPLICA_SET_NAME`

`SHARD_NAME`

`CLUSTER_NAME`

|

`CLUSTER_NAME`

`SHARD_NAME`  
  
matchers

.[n].operator

|

string

|

Optional

|

Comparison operator to apply when checking the current metric value against
**matcher.[n].value**. Atlas accepts the following values:

|

  * `EQUALS`

  * `NOT_EQUALS`

  * `CONTAINS`

  * `NOT_CONTAINS`

|

  * `STARTS_WITH`

  * `ENDS_WITH`

  * `REGEX`

  
|  
  
matchers

.[n].value

|

string

|

Optional

|

Value against which the specified operator compares.

If you set **matchers.[n].fieldName** to `TYPE_NAME`, you can match on the
following values:

|

  * `PRIMARY`

  * `SECONDARY`

  * `STANDALONE`

|

  * `CONFIG`

  * `MONGOS`

  
|  
  
#### Set Notifications

|

|

|  
  
|||  
  
notifications.[n]

.apiToken

|

string

|

Conditional

|

Slack API token.

If the token later becomes invalid, Atlas sends an email to the `Project
Owner` and eventually removes the token.

Set this value if you set `notifications.[n].typeName` to `SLACK`.  
  
notifications.[n]

.channelName

|

string

|

Conditional

|

Slack channel name.

Set this value if you set `notifications.[n].typeName` to `SLACK`.  
  
notifications.[n]

.datadogApiKey

|

string

|

Conditional

|

Datadog API Key. Found in the Datadog dashboard.

Set this value if you set `notifications.[n].typeName` to `DATADOG`.  
  
notifications.[n]

.datadogRegion

|

string

|

Conditional

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

Set this value if you set `notifications.[n].typeName` to `DATADOG`.  
  
notifications.[n]

.delayMin

|

integer

|

Conditional

|

Number of minutes to wait after an alert condition is detected before sending
out the first notification.  
  
notifications.[n]

.emailAddress

|

string

|

Conditional

|

Email address to which alert notifications are sent.

Set this value if you set `notifications.[n].typeName` to `EMAIL`.

You don't need to set this value to send emails to specific users, users with
specific project roles, users with specific organization roles, or teams. Use
the `notifications.[n].emailEnabled` parameter for that purpose.  
  
notifications.[n]

.emailEnabled

|

boolean

|

Conditional

|

Flag indicating if email notifications should be sent to this user's email
address.

Set this value if you set `notifications.[n].typeName` to `GROUP`, `ORG`, or
`USER`.  
  
notifications.[n]

.flowdockApiToken

|

string

|

Conditional

|

Flowdock personal API token.

If the token later becomes invalid, Atlas sends an email to the `Project
Owner` and eventually removes the token.

Set this value if you set `notifications.[n].typeName` to `FLOWDOCK`.  
  
notifications.[n]

.flowName

|

string

|

Conditional

|

Flowdock flow name in lower-case letters. The flow name appears after the
organization name in the URL string:

`www.flowdock.com/app/<organization-name>/<flow-name>`.

Set this value if you set `notifications.[n].typeName` to `FLOWDOCK`.  
  
notifications.[n]

.intervalMin

|

integer

|

Required

|

Number of minutes to wait between successive notifications for unacknowledged
alerts that are not resolved. The minimum value is `5`.

## Note

PagerDuty, VictorOps, and OpsGenie notifications don't return this element.
You must configure and manage the notification interval within each external
service.  
  
notifications.[n]

.mobileNumber

|

string

|

Conditional

|

Mobile number to which alert notifications are sent.

Set this value if you set `notifications.[n].typeName` to `SMS`.

You don't need to set this value to send emails to specific users, users with
specific project roles, users with specific organization roles, or teams. Use
the `notifications.[n].smsEnabled` parameter for that purpose.  
  
notifications.[n]

.notificationToken

|

string

|

Conditional

|

HipChat API token.

Set this value if you set `notifications.[n].typeName` to `HIP_CHAT`.

If the token later becomes invalid, Atlas sends an email to the Project owner
and eventually removes the token.  
  
notifications.[n]

.opsGenieApiKey

|

string

|

Conditional

|

Opsgenie API Key.

If the key later becomes invalid, Atlas sends an email to the `Project Owner`
and eventually removes the key.

Set this value if you set `notifications.[n].typeName` to `OPS_GENIE`.  
  
notifications.[n]

.opsGenieRegion

|

string

|

Conditional

|

Region that indicates the API URL to use. Atlas accepts the following values:

  * `US`

  * `EU`

The default Opsgenie region is `US`.

Set this value if you set `notifications.[n].typeName` to `OPS_GENIE`.  
  
notifications.[n]

.orgName

|

string

|

Conditional

|

Flowdock organization name in lower-case letters. This is the name that
appears after `www.flowdock.com/app/` in the URL string.

Set this value if you set `notifications.[n].typeName` to `FLOWDOCK`.  
  
notifications.[n]

.roles

|

array of strings

|

Conditional

|

One or more roles that receive the configured alert. Atlas accepts the
following values:

|

Project roles

|

Organization roles  
  
|  
  
  * `GROUP_CLUSTER_MANAGER`

  * `GROUP_DATA_ACCESS_ADMIN`

  * `GROUP_DATA_ACCESS_READ_ONLY`

  * `GROUP_DATA_ACCESS_READ_WRITE`

  * `GROUP_OWNER`

  * `GROUP_READ_ONLY`

|

  * `ORG_OWNER`

  * `ORG_MEMBER`

  * `ORG_GROUP_CREATOR`

  * `ORG_BILLING_ADMIN`

  * `ORG_READ_ONLY`

  
  
If you include this field, Atlas sends alerts only to users assigned the roles
you specify in the array. If you omit this field, Atlas sends alerts to users
assigned any role.

Set this value if you set `notifications.[n].typeName` to `GROUP` or `ORG`.  
  
notifications.[n]

.roomName

|

string

|

Conditional

|

HipChat room name.

Set this value if you set `notifications.[n].typeName` to `HIP_CHAT`.  
  
notifications.[n]

.serviceKey

|

string

|

Conditional

|

PagerDuty service key.

If the key later becomes invalid, Atlas sends an email to the `Project Owner`
and eventually removes the key.

Set this value if you set `notifications.[n].typeName` to `PAGER_DUTY`.  
  
notifications.[n]

.smsEnabled

|

boolean

|

Conditional

|

Flag indicating if text message notifications should be sent to this user's
mobile phone.

Set this value if you set `notifications.[n].typeName` to `ORG`, `GROUP`, or
`USER`.  
  
notifications.[n]

.teamId

|

string

|

Conditional

|

Unique identifier of a team.

Set this value if you set `notifications.[n].typeName` to `TEAM`.  
  
notifications.[n]

.typeName

|

string

|

Required

|

Means by which you want Atlas to send you notification of an alert. Atlas
accepts the following values:

|

  * `EMAIL`

  * `SMS`

  * `PAGER_DUTY`

  * `SLACK`

  * `FLOWDOCK`

|

  * `DATADOG`

  * `OPS_GENIE`

  * `VICTOR_OPS`

  * `WEBHOOK`

  * `USER`

|

  * `TEAM`

  * `GROUP` (Project)

  * `ORG`

  * `MICROSOFT_TEAMS`

  
||  
  
notifications.[n]

.username

|

string

|

Conditional

|

Name of the Atlas user to which to send notifications. This user must belong
in the project that owns the alert configuration.

Set this value if you set `notifications.[n].typeName` to `USER`.  
  
notifications.[n]

.victorOpsApiKey

|

string

|

Conditional

|

VictorOps API key.

If the key later becomes invalid, Atlas sends an email to the `Project Owner`
and eventually removes the key.

Set this value if you set `notifications.[n].typeName` to `VICTOR_OPS`.  
  
notifications.[n]

.victorOpsRoutingKey

|

string

|

Conditional

|

VictorOps routing key.

If the key later becomes invalid, Atlas sends an email to the `Project Owner`
and eventually removes the key.

Set this value if you set `notifications.[n].typeName` to `VICTOR_OPS`.  
  
notifications.[n]

.webhookSecret

|

string

|

Conditional

|

Authentication secret for a webhook-based alert.

Atlas returns this value if you set `notifications.[n].typeName` to `WEBHOOK`
and either:

  * You set `notification.[n].webhookSecret` to a non-empty string

  * You set a default `webhookSecret` either on the Integrations page, or with the Integrations API

  
  
notifications.[n]

.webhookUrl

|

string

|

Conditional

|

Target URL for a webhook-based alert.

Atlas returns this value if you set `notifications.[n].typeName` to `WEBHOOK`
and either:

  * You set `notification.[n].webhookURL` to a non-empty string

  * You set a default `webhookUrl` either on the
    Integrations page, or with the Integrations API

  
  
notifications.[n]

.microsoftTeamsWebhookUrl

|

string

|

Conditional

|

Microsoft Teams channel incoming webhook URL.

Set this value if you set `notifications.[n].typeName` to `MICROSOFT_TEAMS`.  
  
## Response Elements

The response includes the alert configuration details:

## Note

Alert configurations vary. An alert configuration may only include a subset of
these elements.

Name

|

Type

|

Description  
  
||  
  
created

|

string

|

Timestamp in ISO 8601 date and time format in UTC when this alert
configuration was created.  
  
enabled

|

boolean

|

Flag indicating this alert configuration enabled.  
  
eventTypeName

|

string

|

Human-readable label that indicates the type of event.  
  
groupId

|

string

|

Unique identifier of the Project that owns this alert configuration.  
  
id

|

string

|

Unique identifier of the alert configuration.  
  
links

|

array of objects

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
matchers

|

array of objects

|

Rules to apply when matching an object against this alert configuration.  
  
matchers

.[n].fieldName

|

string

|

Name of the field in the target object that you wanted this configuration to
match.  
  
matchers

.[n].operator

|

string

|

Comparison operator to apply when checking the current metric value against
`matcher.[n].value`.  
  
matchers

.[n].value

|

string

|

Value to match or exceed using `matchers.[n].operator`.  
  
metricThreshold

|

object

|

Value and means of comparison that triggers an alert.  
  
metricThreshold

.metricName

|

string

|

Name of the metric to check. Supports the same values as the `metricName`
field of the `alerts` resource.

To learn more about the available metrics, see Host Metrics.

## Note

If you set `eventTypeName` to `OUTSIDE_SERVERLESS_METRIC_THRESHOLD`, you can
specify only metrics available for serverless. To learn more, see Serverless
Measurements.  
  
metricThreshold

.mode

|

string

|

Average value of this metric.  
  
metricThreshold

.operator

|

string

|

Comparison operator that Atlas applied when checking the current metric value
against the threshold value.  
  
metricThreshold

.threshold

|

number

|

Value of `metricThreshold.metricName` that, when exceeded, triggers an alert.  
  
metricThreshold

.units

|

string

|

Units of capacity or time that define the scope of the
`metricThreshold.threshold`.  
  
notifications

|

array of objects

|

One or more targets for Atlas to send notifications when an alert condition is
detected.  
  
notifications.[n]

.apiToken

|

string

|

Slack API token token. Atlas returns this value if you set
`notifications.[n].typeName` to `SLACK`.  
  
notifications.[n]

.channelName

|

string

|

Slack channel name. Atlas returns this value if you set
`notifications.[n].typeName` to `SLACK`.  
  
notifications.[n]

.datadogApiKey

|

string

|

DataDog API Key. Atlas returns this value if you set
`notifications.[n].typeName` to `DATADOG`.  
  
notifications.[n]

.datadogRegion

|

string

|

Region that indicates which API URL to use.  
  
notifications.[n]

.delayMin

|

number

|

Number of minutes to wait after an alert condition is detected before sending
out the first notification.  
  
notifications.[n]

.emailAddress

|

string

|

Email address to which to send notification. Atlas returns this value if you
set `notifications.[n].typeName` to `EMAIL`.  
  
notifications.[n]

.emailEnabled

|

boolean

|

Flag indicating email notifications must be sent. Atlas returns this value if
you set `notifications.[n].typeName` to `ORG`, `GROUP`, or `USER`.  
  
notifications.[n]

.flowdockApiToken

|

string

|

Flowdock personal API token. Atlas returns this value if you set
`notifications.[n].typeName` to `FLOWDOCK`.  
  
notifications.[n]

.flowName

|

string

|

Name of the Flowdock flow. Atlas returns this value if you set
`notifications.[n].typeName` to `FLOWDOCK`.  
  
notifications.[n]

.intervalMin

|

number

|

Number of minutes to wait between successive notifications for unacknowledged
alerts that are not resolved.

## Note

PagerDuty, VictorOps, and OpsGenie notifications don't return this element.
You must configure and manage the notification interval within each external
service.  
  
notifications.[n]

.mobileNumber

|

string

|

Mobile number to which alert notifications are sent. Atlas returns this value
if you set `notifications.[n].typeName` to `SMS`.  
  
notifications.[n]

.microsoftTeamsWebhookUrl

|

string

|

Microsoft Teams incoming webhook URL. Atlas returns this value if you set
`notifications.[n].typeName` to `MICROSOFT_TEAMS`.  
  
notifications.[n]

.notificationToken

|

string

|

HipChat API token. Atlas returns this value if you set
`notifications.[n].typeName` to `HIP_CHAT`.

If the token later becomes invalid, Atlas sends an email to the `Project
Owner` and eventually removes the token.  
  
notifications.[n]

.opsGenieApiKey

|

string

|

Opsgenie API Key. Atlas returns this value if you set
`notifications.[n].typeName` to `OPS_GENIE`.  
  
notifications.[n]

.opsGenieRegion

|

string

|

Region that indicates which API URL to use. Atlas returns this value if you
set `notifications.[n].typeName` to `OPS_GENIE`.  
  
notifications.[n]

.orgName

|

string

|

Name of the Flowdock organization. Atlas returns this value if you set
`notifications.[n].typeName` to `FLOWDOCK`.  
  
notifications.[n]

.roles

|

array of strings

|

Atlas role in current Project or Organization. Atlas returns this value if you
set `notifications.[n].typeName` to `ORG` or `GROUP`.  
  
notifications.[n]

.roomName

|

string

|

HipChat room name. Atlas returns this value if `"notifications.typeName" :
"HIP_CHAT`.  
  
notifications.[n]

.serviceKey

|

string

|

PagerDuty service key. Atlas returns this value if you set
`notifications.[n].typeName` to `PAGER_DUTY`.  
  
notifications.[n]

.smsEnabled

|

boolean

|

Flag indicating text notifications must be sent. Atlas returns this value if
you set `notifications.[n].typeName` to `ORG`, `GROUP`, or `USER`.  
  
notifications.[n]

.teamId

|

string

|

Unique identifier of the team that receives this notification.  
  
notifications.[n]

.teamName

|

string

|

Label for the team that receives this notification.  
  
notifications.[n]

.typeName

|

string

|

Means by which you want Atlas to send you notification of an alert.  
  
notifications.[n]

.username

|

string

|

Name of an Atlas user to which to send notifications. Atlas returns this value
if you set `notifications.[n].typeName` to `USER`.  
  
notifications.[n]

.victorOpsApiKey

|

string

|

VictorOps API key.

If the key later becomes invalid, Atlas sends an email to the `Project Owner`
and eventually removes the key.

Atlas returns this value if you set `notifications.[n].typeName` to
`VICTOR_OPS`.  
  
notifications.[n]

.victorOpsRoutingKey

|

string

|

VictorOps routing key.

If the key later becomes invalid, Atlas sends an email to the `Project Owner`
and eventually removes the key.

Atlas returns this value if you set `notifications.[n].typeName` to
`VICTOR_OPS`.  
  
notifications.[n]

.webhookSecret

|

string

|

Authentication secret for a webhook-based alert.

Atlas returns this value if you set `notifications.[n].typeName` to `WEBHOOK`
and either:

  * You set `notification.[n].webhookSecret` to a non-empty string

  * You set a default `webhookSecret` either on the Integrations page, or with the Integrations API

  
  
notifications.[n]

.webhookUrl

|

string

|

Target URL for a webhook-based alert.

Atlas returns this value if you set `notifications.[n].typeName` to `WEBHOOK`
and either:

  * You set `notification.[n].webhookURL` to a non-empty string

  * You set a default `webhookUrl` either on the
    Integrations page, or with the Integrations API

  
  
threshold

|

object

|

Threshold that triggers an alert. Atlas returns this value if `eventTypeName`
is any value other than `OUTSIDE_METRIC_THRESHOLD`.  
  
threshold

.operator

|

string

|

Comparison operator that Atlas applied when checking the current metric value
against the threshold value.  
  
threshold

.threshold

|

number

|

Value that, when exceeded, Atlas triggers an alert.  
  
threshold

.units

|

string

|

Units of capacity or time that define the scope of the `threshold.threshold`.  
  
typeName

|

string

|

 _This field is deprecated and is ignored._  
  
updated

|

string

|

Timestamp in ISO 8601 date and time format in UTC when this alert
configuration was last updated.  
  
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

Condition

Metrics

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --request PUT "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}alertConfigs/{ALERT-CONFIG-ID}?pretty=true" \  
    3|      --header "Content-Type: application/json" \  
    4|      --data '  
    5|        {  
    6|          "eventTypeName" : "REPLICATION_OPLOG_WINDOW_RUNNING_OUT",  
    7|          "enabled" : true,  
    8|          "notifications" : [ {  
    9|            "delayMin" : 0,  
    10|            "emailEnabled" : true,  
    11|            "intervalMin" : 15,  
    12|            "roles" : [ "GROUP_OWNER" ],  
    13|            "smsEnabled" : false,  
    14|            "typeName" : "GROUP"  
    15|          } ],  
    16|          "threshold" : {  
    17|            "operator" : "LESS_THAN",  
    18|            "threshold" : 1  
    19|          },  
    20|          "typeName" : "REPLICA_SET"  
    21|        }'  
  
## Example Response

Condition

Metrics

    
    
    1| {  
    |  
    2|   "created" : "2020-02-26T01:34:52Z",  
    3|   "enabled" : true,  
    4|   "eventTypeName" : "REPLICATION_OPLOG_WINDOW_RUNNING_OUT",  
    5|   "groupId" : "{GROUP-ID}",  
    6|   "id" : "{ALERT-CONFIG-ID}",  
    7|   "links" : [ {  
    8|     "href" : "https://cloud.mongodb.com/api/public/v1.0/groups/{GROUP-ID}/alertConfigs/{ALERT-CONFIG-ID}",  
    9|     "rel" : "self"  
    10|   }, {  
    11|     "href" : "https://cloud.mongodb.com/api/public/v1.0/groups/{GROUP-ID}/alertConfigs/{ALERT-CONFIG-ID}/alerts",  
    12|     "rel" : "http://mms.mongodb.com/alerts"  
    13|   } ],  
    14|   "matchers" : [ ],  
    15|   "notifications" : [ {  
    16|     "delayMin" : 0,  
    17|     "emailEnabled" : true,  
    18|     "intervalMin" : 15,  
    19|     "roles" : [ "GROUP_OWNER" ],  
    20|     "smsEnabled" : false,  
    21|     "typeName" : "GROUP"  
    22|   } ],  
    23|   "threshold" : {  
    24|     "operator" : "LESS_THAN",  
    25|     "threshold" : 1  
    26|   },  
    27|   "typeName" : "REPLICA_SET",  
    28|   "updated" : "2020-02-26T01:34:52Z"  
    29| }  
  
What is MongoDB Atlas? →

