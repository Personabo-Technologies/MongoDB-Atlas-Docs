Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `AtlasProject` Custom Resource

Share Feedback

On this page

  * Example
  * Prometheus Example
  * Teams Example
  * Maintenance Window Example
  * Project Settings Example
  * Alert Configuration Example
  * Parameters

The `AtlasProject` custom resource configures the project in Atlas. When you
create the `AtlasProject` custom resource, Atlas Kubernetes Operator tries to
create a new project in Atlas.

## Important

### Custom Resources Definitions Take Priority

Atlas Kubernetes Operator uses custom resource configuration files to manage
your Atlas configuration. Each custom resource definition overrides settings
specified in other ways such as in the Atlas UI. If you delete a custom
resource, Atlas Kubernetes Operator deletes the object from Atlas unless you
use annotations to skip deletion. To learn more, see the Create and Update
Process and the Delete Process.

Atlas Kubernetes Operator does one of the following actions:

  * Creates a new project in the organization that the connection secret configures.

  * Reuses an existing project. In this case, Atlas Kubernetes Operator verifies whether a project with `spec.name` exists. If the project exists, Atlas Kubernetes Operator skips creation. After the reconciliation, Atlas Kubernetes Operator updates the `status.id` field with the id of the project.

You can use the `spec.connectionSecretRef.name` parameter to set the
connection secret for the `AtlasProject` custom resource. This parameter
overrides the default `global` connection secret.

## Note

By default, Atlas Kubernetes Operator keeps connection secrets in the same
namespace as the `AtlasProject` Custom Resource. To store secrets in another
namespace, specify the `spec.connectionSecretRef.namespace` parameter.

To connect to the Atlas Administration API, Atlas Kubernetes Operator reads
the organization ID and API keys from Atlas Kubernetes Operator secrets.

You can also edit the `AtlasProject` custom resource specification to
configure the following options:

  * An IP access list with the `spec.projectIpAccessList` parameter. This IP access list grants network access to Atlas clusters in the project.

  * Teams with the `spec.teams` parameter. A team lets you grant an access role to an entire group of Atlas users for a particular project.

  * The maintenance window with the `spec.maintenanceWindow` parameter. The maintenance window sets the hour and day that Atlas starts weekly maintenance on your database deployments.

  * Network peering with the `spec.networkPeers` parameter. Network peering allows you to connect securely to your AWS, Azure, or Google Cloud VPC.

  * Encryption at rest using customer-managed keys with the `spec.encryptionAtRest` parameter. Encryption at rest using customer-managed keys allows you to add an additional layer of security by using your cloud provider's KMS together with the MongoDB encrypted storage engine.

  * Private endpoints with the `spec.privateEndpoints` parameter.

  * X.509 authentication with the `spec.X509CertRef.name` parameter.

  * Project settings with the `spec.settings` parameter, including settings to enable and disable the following:

    * Collection of database statistics in cluster metrics

    * Data explorer

    * Performance Advisor

    * Realtime Performance Panel

    * Schema Advisor

    * Project alerts configurations with the `spec.alertConfigurationSyncEnabled` and `spec.alertConfigurations` parameters.

For information on how these settings interact, see the Considerations.

If you remove the `AtlasProject` resource from your Kubernetes cluster, Atlas
Kubernetes Operator removes the project from Atlas. You must remove all the
clusters in the project beforehand. Otherwise, Atlas rejects the delete
request.

## Example

The following example shows an `AtlasProject` custom resource specification:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasProject  
    metadata:  
     name: my-project  
     labels:  
       ​​app.kubernetes.io/version: 1.6.0  
    spec:  
     name: Test project  
     connectionSecretRef:  
       name: my-atlas-key  
       label: atlas.mongodb.com/type=credentials  
     projectIpAccessList:  
       - ipAddress: "192.0.2.15"  
         comment: "IP address for Application Server A"  
       - cidrBlock: "203.0.113.0/24"  
         comment: "CIDR block for Application Server B - D"  
  
## Prometheus Example

The following example shows an `AtlasProject` custom resource specification
that integrates with Prometheus:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
       ​​app.kubernetes.io/version: 1.6.0  
    spec:  
      name: TestPrometheusIntegration  
      connectionSecretRef:  
        name: my-atlas-key  
      projectIpAccessList:  
        - ipAddress: "0.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
        - ipAddress: "128.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
      integrations:  
        - type: "PROMETHEUS"  
          enabled: "true"  
          username: "prometheus-user"  
          passwordRef:  
            name: "password-name"  
            namespace: "password-namespace"  
          scheme: "http"  
          serviceDiscovery: "http"  
  
To learn more, see Integrate with Third-Party Services.

## Note

Atlas Kubernetes Operator offers a sample Grafana dashboard that you can
import into Grafana.

## Teams Example

The following example shows an `AtlasProject` custom resource specification
that gives the `green-leaf-team` the `Organization Owner` role for this
project. The team members are defined in the AtlasTeam custom resource.

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
       ​​app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test project  
      teams:  
        - teamRef:  
            name: green-leaf-team  
          roles:  
          - ORGANIZATION_OWNER  
  
To learn more, see Configure Teams.

## Maintenance Window Example

The following example shows an `AtlasProject` custom resource specification
that sets the maintenance window to 5:00 AM every Tuesday with automatic
deferral disabled:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasProject  
    metadata:  
     name: my-project  
     labels:  
       ​​app.kubernetes.io/version: 1.6.0  
    spec:  
     name: Test project  
     projectIpAccessList:  
       - ipAddress: "192.0.2.15"  
         comment: "IP address for Application Server A"  
    maintenanceWindow:  
     dayOfWeek: 3  
     hourOfDay: 5  
     autoDefer: false  
  
## Project Settings Example

The following example shows an `AtlasProject` custom resource specification
that disables the collection of database statistics in cluster metrics, data
explorer, Performance Advisor, Realtime Performance Panel, and Schema Advisor.

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasProject  
    metadata:  
     name: my-project  
     labels:  
       ​​app.kubernetes.io/version: 1.6.0  
    spec:  
     name: Test project  
     projectIpAccessList:  
       - ipAddress: "192.0.2.15"  
         comment: "IP address for Application Server A"  
     settings:  
       isCollectDatabaseSpecificsStatisticsEnabled: false  
       isDataExplorerEnabled: false  
       isPerformanceAdvisorEnabled: false  
       isRealtimePerformancePanelEnabled: false  
       isSchemaAdvisorEnabled: false  
  
## Alert Configuration Example

The following example shows an `AtlasProject` custom resource specification
that configures an alert that triggers if the oplog window reaches less than
one hour:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
       ​​app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Atlas Operator Project  
      connectionSecretRef:  
        name: my-atlas-key  
      alertConfigurations:  
        - eventTypeName: "REPLICATION_OPLOG_WINDOW_RUNNING_OUT",  
          enabled: true,  
          notifications:  
          -  delayMin: 0  
             emailEnabled: true  
             intervalMin: 60  
             roles: [ "GROUP_OWNER" ]  
             smsEnabled: false  
             typeName: “GROUP”  
          threshold:  
             operator: "LESS_THAN",  
             threshold: 1,  
             units: "HOURS"  
      alertConfigurationSyncEnabled: true  
      withDefaultAlertsSettings: false  
  
## Parameters

This section describes the `AtlasProject` custom resource parameters:

`spec.name`

    

 _Type_ : string

 _Required_

Name of the project created or updated in Atlas. The name length must not
exceed 64 characters. The name can contain only letters, numbers, spaces,
dashes, and underscores.

`spec.alertConfigurations`

    

 _Type: array of objects_

 _Optional_

List that contains alert configurations for this project.

If you use this setting, you must also set
`spec.alertConfigurationSyncEnabled` to `true` for Atlas Kubernetes Operator
to modify project alert configurations.

If you omit or leave this setting empty, Atlas Kubernetes Operator doesn't
alter the project's alert configurations. If creating a project, Atlas applies
the default project alert configurations.

`spec.alertConfigurations.eventTypeName`

    

 _Type: string_

 _Required_

Event that triggers an alert that this alert configration describes.

To learn about the values that Atlas Kubernetes Operator accepts, see the
request body schema for the Create One Alert Configuration in One Project
endpoint in the MongoDB Atlas Administration API documentation.

`spec.alertConfigurations.enabled`

    

 _Type: boolean_

 _Optional_

 _Default_ : `false`

Flag that indicates whether this alert configuration is enabled. If omitted,
defaults to `false`.

`spec.alertConfigurations.matchers`

    

 _Type: array of objects_

 _Conditional_

List of rules that determine whether Atlas checks an object for the alert
configuration. You can filter using the matchers array if
`spec.alertConfigurations.eventTypeName` specifies an event for a host,
replica set, or sharded cluster.

`spec.alertConfigurations.matchers.fieldName`

    

 _Type: string_

 _Conditional_

Human-readable label that identifies the parameter in the target object that
Atlas checks. The parameter must match all rules for Atlas to check for alert
configurations.

Atlas Kubernetes Operator accepts the following values:

  * `CLUSTER_NAME`

  * `HOSTNAME`

  * `HOSTNAME_AND_PORT`

  * `PORT`

  * `REPLICA_SET_NAME`

  * `SHARD_NAME`

  * `TYPE_NAME`

Atlas Kubernetes Operator requires this setting if you include an object in
the `spec.alertConfigurations.matchers` array.

`spec.alertConfigurations.matchers.operator`

    

 _Type: string_

 _Conditional_

Comparison operator to apply when checking the current metric value against
`spec.alertConfigurations.matchers.value`.

Atlas Kubernetes Operator accepts the following values:

  * `EQUALS`

  * `CONTAINS`

  * `STARTS_WITH`

  * `ENDS_WITH`

  * `NOT_EQUALS`

  * `NOT_CONTAINS`

  * `REGEX`

Atlas Kubernetes Operator requires this setting if you include an object in
the `spec.alertConfigurations.matchers` array.

`spec.alertConfigurations.matchers.value`

    

 _Type: string_

 _Conditional_

Value to match or exceed using the specified
`spec.alertConfigurations.matchers.operator`.

Atlas Kubernetes Operator requires this setting if you include an object in
the `spec.alertConfigurations.matchers` array.

`spec.alertConfigurations.metricThreshold`

    

 _Type: object_

 _Conditional_

Threshold for the metric that, when exceeded, triggers an alert.

Atlas Kubernetes Operator requires this setting when
`spec.alertConfigurations.eventTypeName` is `OUTSIDE_METRIC_THRESHOLD`.

`spec.alertConfigurations.metricThreshold.metricName`

    

 _Type: string_

 _Conditional_

Human-readable label that identifies the metric against which Atlas checks the
configured `spec.alertConfigurations.metricThreshold.threshold`.

To learn about the values that Atlas Kubernetes Operator accepts, see the
request body schema for the Create One Alert Configuration in One Project
endpoint in the MongoDB Atlas Administration API documentation.

Atlas Kubernetes Operator requires this setting if you include the
`spec.alertConfigurations.metricThreshold` object.

`spec.alertConfigurations.metricThreshold.mode`

    

 _Type: string_

 _Optional_

 _Default_ : `AVERAGE`

Atlas computes the current metric value as an average.

Atlas Kubernetes Operator accepts only a value of `AVERAGE`.

`spec.alertConfigurations.metricThreshold.operator`

    

 _Type: string_

 _Conditional_

Comparison operator to apply when checking the current metric value.

Atlas Kubernetes Operator accepts the following values:

  * `GREATER_THAN`

  * `LESS_THAN`

Atlas Kubernetes Operator requires this setting if you include the
`spec.alertConfigurations.metricThreshold` object.

`spec.alertConfigurations.metricThreshold.threshold`

    

 _Type: integer_

 _Conditional_

Value of metric that, when exceeded, triggers an alert.

Atlas Kubernetes Operator requires this setting if you include the
`spec.alertConfigurations.metricThreshold` object.

`spec.alertConfigurations.metricThreshold.units`

    

 _Type: string_

 _Conditional_

Element used to express the quantity. This value can be an element of time,
storage capacity, and so on

Atlas Kubernetes Operator accepts the following values:

  * `BITS`

  * `BYTES`

  * `DAYS`

  * `GIGABITS`

  * `GIGABYTES`

  * `HOURS`

  * `KILOBITS`

  * `KILOBYTES`

  * `MEGABITS`

  * `MEGABYTES`

  * `MILLISECONDS`

  * `MINUTES`

  * `PETABYTES`

  * `RAW`

  * `SECONDS`

  * `TERABYTES`

Atlas Kubernetes Operator requires this setting if you include the
`spec.alertConfigurations.metricThreshold` object.

`spec.alertConfigurations.notifications`

    

 _Type: array_

 _Conditional_

List that describes the notifications that Atlas sends for alerts that this
alert configuration describes.

`spec.alertConfigurations.notifications.apiToken`

    

 _Type: string_

 _Conditional_

Slack API token or Bot token that Atlas needs to send alert notifications via
Slack. If the token later becomes invalid, Atlas sends an email to the project
owners. If the token remains invalid, Atlas removes the token.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `SLACK`.

`spec.alertConfigurations.notifications.channelName`

    

 _Type: string_

 _Conditional_

Human-readable label that identifies the Slack channel to which Atlas sends
alert notifications.

Atlas Kubernetes Operator requires this setting when you set
`spec.alertConfigurations.notifications.typeName` to `SLACK`.

`spec.alertConfigurations.notifications.datadogApiKey`

    

 _Type: string_

 _Conditional_

Datadog API key that Atlas needs to send alert notifications to Datadog. You
can find this API key in the Datadog dashboard.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `DATADOG`.

`spec.alertConfigurations.notifications.datadogRegion`

    

 _Type: string_

 _Optional_

 _Default_ : `US`

Datadog region that indicates which API Uniform Resource Locator (URL) to use.

Atlas Kubernetes Operator accepts the following values:

  * `US`

  * `EU`

`spec.alertConfigurations.notifications.delayMins`

    

 _Type: integer_

 _Optional_

 _Default_ : `0`

Number of minutes that Atlas waits after it detects an alert condition before
it sends out the first notification.

`spec.alertConfigurations.notifications.emailAddress`

    

 _Type: string_

 _Conditional_

Email address to which Atlas sends alert notifications.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `EMAIL`.

Atlas Kubernetes Operator doesn't require this setting to send email
notifications when you set `spec.alertConfigurations.notifications.typeName`
to one of the following values:

  * `GROUP`

  * `ORG`

  * `TEAM`

  * `USERS`

To send emails to one Atlas user or group of users, set the
`spec.alertConfigurations.notifications.emailEnabled` parameter.

`spec.alertConfigurations.notifications.emailEnabled`

    

 _Type: boolean_

 _Conditional_

Flag that indicates whether Atlas sends email notifications.

Atlas Kubernetes Operator requires this setting when you set
`spec.alertConfigurations.notifications.typeName` to one of the following
values:

  * `GROUP`

  * `ORG`

  * `TEAM`

`spec.alertConfigurations.notifications.intervalMin`

    

 _Type: integer_

 _Optional_

Number of minutes to wait between successive notifications. Atlas sends
notifications until someone acknowledges the unacknowledged alert. Atlas
Kubernetes Operator accepts values greater than or equal to `5`.

PagerDuty, VictorOps, and OpsGenie notifications don't use this field.
Configure and manage the notification interval within each of those services.

`spec.alertConfigurations.notifications.microsoftTeamsWebhookUrl`

    

 _Type: string_

 _Conditional_

Microsoft Teams Webhook Uniform Resource Locator (URL) that Atlas needs to
send this notification via Microsoft Teams. If the URL later becomes invalid,
Atlas sends an email to the project owners. If the key remains invalid, Atlas
removes it.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `MICROSOFT_TEAMS`.

`spec.alertConfigurations.notifications.mobileNumber`

    

 _Type: string_

 _Conditional_

Mobile phone number to which Atlas sends alert notifications.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `SMS`.

`spec.alertConfigurations.notifications.opsGenieApiKey`

    

 _Type: string_

 _Conditional_

API Key that Atlas needs to send this notification via Opsgenie. If the key
later becomes invalid, Atlas sends an email to the project owners. If the key
remains invalid, Atlas removes it.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `OPS_GENIE`.

`spec.alertConfigurations.notifications.opsGenieRegion`

    

 _Type: string_

 _Optional_

 _Default_ : `US`

Opsgenie region that indicates which API Uniform Resource Locator (URL) to
use.

Atlas Kubernetes Operator accepts the following values:

  * `US`

  * `EU`

Atlas Kubernetes Operator applies this setting if you set
`spec.alertConfigurations.notifications.typeName` to `OPS_GENIE`.

`spec.alertConfigurations.notifications.roles`

    

 _Type: array_

 _Optional_

List that contains the one or more organization or project roles that receive
the configured alert. If you include this parameter, Atlas sends alerts only
to users assigned the roles you specify in the list. If you omit this
parameter, Atlas sends alerts to users assigned any role.

Atlas Kubernetes Operator accepts the following values:

  * `GROUP_CLUSTER_MANAGER`

  * `GROUP_DATA_ACCESS_ADMIN`

  * `GROUP_DATA_ACCESS_READ_ONLY`

  * `GROUP_DATA_ACCESS_READ_WRITE`

  * `GROUP_OWNER`

  * `GROUP_READ_WRITE`

  * `ORG_OWNER`

  * `ORG_MEMBER`

  * `ORG_GROUP_CREATOR`

  * `ORG_BILLING_ADMIN`

  * `ORG_READ_ONLY`

Atlas Kubernetes Operator applies this setting when you set
`spec.alertConfigurations.notifications.typeName` to one of the following
values:

  * `GROUP`

  * `ORG`

`spec.alertConfigurations.notifications.serviceKey`

    

 _Type: string_

 _Conditional_

PagerDuty service key that Atlas needs to send notifications via PagerDuty. If
the key later becomes invalid, Atlas sends an email to the project owners. If
the key remains invalid, Atlas removes it.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `PAGER_DUTY`.

`spec.alertConfigurations.notifications.severity`

    

 _Type: string_

 _Optional_

Degree of seriousness given to this notification.

Atlas Kubernetes Operator accepts the following values:

  * `CRITICAL`

  * `ERROR`

  * `WARNING`

`spec.alertConfigurations.notifications.smsEnabled`

    

 _Type: boolean_

 _Conditional_

Flag that indicates whether Atlas sends text message notifications.

Atlas Kubernetes Operator requires this setting when you set
`spec.alertConfigurations.notifications.typeName` to one of the following
values:

  * `GROUP`

  * `ORG`

  * `TEAM`

`spec.alertConfigurations.notifications.teamId`

    

 _Type: string_

 _Conditional_

Unique 24-hexadecimal digit string that identifies one Atlas team.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `TEAM`.

`spec.alertConfigurations.notifications.teamName`

    

 _Type: string_

 _Conditional_

Name of the Atlas team that receives this notification.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `TEAM`.

`spec.alertConfigurations.notifications.typeName`

    

 _Type: string_

 _Conditional_

Human-readable label that displays the alert notification type. This setting
is required if you specify a value for the
`spec.alertConfigurations.notifications` setting. Atlas supports the following
values:

  * `DATADOG`

  * `EMAIL`

  * `OPS-GENIE`

  * `ORG`

  * `PAGER_DUTY`

  * `PROMETHEUS`

  * `SLACK`

  * `SMS`

  * `TEAM`

  * `USER`

  * `VICTOR_OPS`

  * `WEBHOOK`

`spec.alertConfigurations.notifications.username`

    

 _Type: string_

 _Conditional_

Atlas username of the person to whom Atlas sends notifications. Specify only
Atlas users who belong to the project that owns the alert configuration.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `USER`.

`spec.alertConfigurations.notifications.victorOpsApiKey`

    

 _Type: string_

 _Conditional_

API key that Atlas needs to send alert notifications to Splunk On-Call. If the
key later becomes invalid, Atlas sends an email to the project owners. If the
key remains invalid, Atlas removes it.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `VICTOR_OPS`.

`spec.alertConfigurations.notifications.victorOpsRoutingKey`

    

 _Type: string_

 _Conditional_

Routing key that Atlas needs to send alert notifications to Splunk On-Call. If
the key later becomes invalid, Atlas sends an email to the project owners. If
the key remains invalid, Atlas removes it.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `VICTOR_OPS`.

`spec.alertConfigurations.notifications.webhookSecret`

    

 _Type: string_

 _Optional_

Authentication secret for a webhook-based alert.

Atlas Kubernetes Operator applies this setting if you set
`spec.alertConfigurations.notifications.typeName` to `WEBHOOK`.

`spec.alertConfigurations.notifications.webhookUrl`

    

 _Type: string_

 _Conditional_

String that indicates your webhook URL.

Atlas Kubernetes Operator requires this setting if you set
`spec.alertConfigurations.notifications.typeName` to `WEBHOOK`.

`spec.alertConfigurations.threshold`

    

 _Type: object_

 _Conditional_

Limit that triggers an alert when exceeded.

Atlas Kubernetes Operator applies this setting if you set
`spec.alertConfigurations.eventTypeName` to a value other than
`OUTSIDE_METRIC_THRESHOLD`.

`spec.alertConfigurations.threshold.operator`

    

 _Type: string_

 _Conditional_

Comparison operator to apply when Atlas checks the current metric value.

Atlas Kubernetes Operator accepts the following values:

  * `GREATER_THAN`

  * `LESS_THAN`

Atlas Kubernetes Operator requires this setting if you include the
`spec.alertConfigurations.threshold` object.

`spec.alertConfigurations.threshold.threshold`

    

 _Type: integer_

 _Conditional_

Value of metric that, when exceeded, triggers an alert.

Atlas Kubernetes Operator requires this setting if you include the
`spec.alertConfigurations.threshold` object.

`spec.alertConfigurations.threshold.units`

    

 _Type: string_

 _Conditional_

Element that expresses the quantity. You can specify an element of time,
storage capacity, and so on.

Atlas Kubernetes Operator accepts the following values:

  * `BITS`

  * `BYTES`

  * `DAYS`

  * `GIGABITS`

  * `GIGABYTES`

  * `HOURS`

  * `KILOBITS`

  * `KILOBYTES`

  * `MEGABITS`

  * `MEGABYTES`

  * `MILLISECONDS`

  * `MINUTES`

  * `PETABYTES`

  * `RAW`

  * `SECONDS`

  * `TERABYTES`

Atlas Kubernetes Operator requires this setting if you include the
`spec.alertConfigurations.threshold` object.

`spec.alertConfigurationSyncEnabled`

    

 _Type: boolean_

 _Optional_

 _Default_ : `false`

Flag that indicates whether Atlas Kubernetes Operator applies the project
alert settings defined in `spec.alertConfigurations`. If you omit or set to
this parameter to `false`, Atlas Kubernetes Operator doesn't syncronize the
project's alert configurations with the ones that you define in the
`AtlasProject` custom resource.

For information on how this setting interacts with
`spec.withDefaultAlertsSettings`, see the Considerations.

`spec.auditing.auditAuthorizationSuccess`

    

 _Type_ : boolean

 _Optional_

 _Default_ : `false`

Flag that indicates whether to direct the auditing system to capture
successful authentication attempts for audit filters using the `"atype" :
"authCheck"` auditing event. To set this parameter to `true`, you must set
`spec.auditing.enabled` to `true`. To learn more, see
auditAuthorizationSuccess.

## Warning

If you enable auditAuthorizationSuccess, you might severely impact cluster
performance. Enable this option with caution.

`spec.auditing.auditFilter`

    

 _Type_ : string

 _Optional_

JSON-formatted auditing filter. You might need to escape the JSON string to
remove characters that could prevent parsing, such as single or double-quotes.
To specify a value for this setting, you must set `spec.auditing.enabled` to
`true`.

To view example auditing filters, see Example Auditing Filters. To learn more
about configuring MongoDB auditing filters, see Configure a Custom Auditing
Filter.

`spec.auditing.enabled`

    

 _Type_ : boolean

 _Conditional_

 _Default_ : `false`

Flag that indicates whether to enable auditing for the project. To specify a
value for `spec.auditing.auditFilter`, or to set
`spec.auditing.auditAuthorizationSuccess` to `true`, you must specify this
setting. To learn more, see Enable Audit Logs.

`spec.connectionSecretRef.name`

    

 _Type_ : string

 _Optional_

Name of the secret with the organization ID and API keys that Atlas Kubernetes
Operator uses to connect to Atlas. If unspecified, Atlas Kubernetes Operator
uses the default `global` secret.

## Note

By default, Atlas Kubernetes Operator keeps connection secrets in the same
namespace as the `AtlasProject` Custom Resource. To store secrets in another
namespace, specify the `spec.connectionSecretRef.namespace` parameter.

`spec.connectionSecretRef.namespace`

    

 _Type_ : string

 _Optional_

Namespace that contains the secret with the organization ID and API keys that
Atlas Kubernetes Operator uses to connect to Atlas. If unspecified, Atlas
Kubernetes Operator keeps connection secrets in the same namespace as the
`AtlasProject` Custom Resource.

`spec.cloudProviderAccessRoles`

    

 _Type_ : array

 _Optional_

List that contains your unified cloud provider access settings.

`spec.cloudProviderAccessRoles.iamAssumedRoleArn`

    

 _Type_ : string

 _Conditional_

Unique AWS ARN that identifies the IAM access role that Atlas assumes. If you
want to set up unified cloud provider access, you must specify this setting.

`spec.cloudProviderAccessRoles.providerName`

    

 _Type_ : string

 _Conditional_

Cloud provider for the access role that Atlas assumes. Atlas Kubernetes
Operator supports `AWS` for unified cloud provider access. If you want to set
up unified cloud provider access, you must specify this setting.

`spec.customRoles`

    

 _Type_ : object

 _Optional_

Object that contains your custom role specifications. To learn more, see
Configure Custom Database Roles.

`spec.customRoles.roleName`

    

 _Type_ : string

 _Optional_

Human-readable label that identifies the custom role.

## Important

The specified role name can only contain letters, digits, underscores, and
dashes. Additionally, you cannot specify a role name which meets any of the
following criteria:

  * Is a name already used by an existing custom role in the project

  * Is a name of any of the built-in roles

  * Is `atlasAdmin`

  * Starts with `xgen-`

`spec.customRoles.actions`

    

 _Type_ : array

 _Optional_

List of objects that represents the individual privilege actions that the role
grants.

`spec.customRoles.actions.action`

    

 _Type_ : string

 _Optional_

Human-readable label that identifies the privilege action. For a complete list
of actions available in the Atlas Administration API, see Custom Role Actions.

`spec.customRoles.actions.resources`

    

 _Type_ : array

 _Optional_

List of objects that indicate a database and collection on which the action is
granted, or indicates that the action is granted on the cluster resource.

`spec.customRoles.actions.resources.cluster`

    

 _Type_ : boolean

 _Optional_

Flag that indicates that the action is granted on the cluster resource.

## Note

This parameter is mutually exclusive with the
`spec.customRoles.actions.resources.collection` and
`spec.customRoles.actions.resources.db` parameters.

`spec.customRoles.actions.resources.collection`

    

 _Type_ : string

 _Optional_

Human-readable label that identifies the collection on which the action is
granted. If this value is an empty string, the action is granted on all
collections within the database specified in the
`spec.customRoles.actions.resources.db` parameter.

## Note

This parameter is mutually exclusive with the
`spec.customRoles.actions.resources.cluster` parameter.

`spec.customRoles.actions.resources.db`

    

 _Type_ : string

 _Optional_

Human-readable label that indentifies the database on which the action is
granted.

## Note

This parameter is mutually exclusive with the
`spec.customRoles.actions.resources.cluster` parameter.

`spec.customRoles.inheritedRoles`

    

 _Type_ : array

 _Optional_

List of objects that represent key-value pairs that indicate the inherited
role and the database on which the role is granted.

`spec.customRoles.inheritedRoles.db`

    

 _Type_ : string

 _Optional_

Human-readable label that identifies the database on which the inherited role
is granted.

## Note

This value should be `admin` for all roles except read and readWrite.

`spec.customRoles.inheritedRoles.role`

    

 _Type_ : string

 _Optional_

Human-readable label that identifies the inherited role. You can specify
another custom role or a built-in role.

`spec.encryptionAtRest`

    

 _Type_ : array

 _Optional_

List that contains the configurations for encryption at rest using customer-
managed keys for the project.

`spec.encryptionAtRest.awsKms`

    

 _Type_ : object

 _Optional_

List that contains the configurations to use AWS KMS for encryption at rest
using customer-managed keys for the project.

`spec.encryptionAtRest.azureKeyVault`

    

 _Type_ : object

 _Optional_

List that contains the configurations to use Azure Key Vault for encryption at
rest using customer-managed keys for the project.

`spec.encryptionAtRest.googleCloudKms`

    

 _Type_ : object

 _Optional_

List that contains the configurations to use Google Cloud KMS for encryption
at rest using customer-managed keys for the project.

`spec.integrations`

    

 _Type_ : array

 _Optional_

List that contains your third-party integration settings. The parameters that
you must specify depend on the third-party service that you want to configure:

Service

|

Settings  
  
|  
  
All

|

  * `spec.integrations.type`

  
  
Datadog

|

  * `spec.integrations.apiKeyRef.name`

  * `spec.integrations.apiKeyRef.namespace`

  * `spec.integrations.region`

  
  
Flowdock

|

  * `spec.integrations.apiTokenRef.name`

  * `spec.integrations.apiTokenRef.namespace`

  * `spec.integrations.flowName`

  * `spec.integrations.orgName`

  
  
Microsoft Teams

|

  * `spec.integrations.microsoftTeamsWebhookURL`

  
  
Opsgenie

|

  * `spec.integrations.apiKeyRef.name`

  * `spec.integrations.apiKeyRef.namespace`

  * `spec.integrations.region`

  
  
PagerDuty

|

  * `spec.integrations.serviceKeyRef.name`

  * `spec.integrations.serviceKeyRef.namespace`

  
  
Prometheus

|

  * `spec.integrations.enabled`

  * `spec.integrations.passwordRef.name`

  * `spec.integrations.passwordRef.namespace`

  * `spec.integrations.scheme`

  * `spec.integrations.serviceDiscovery`

  * `spec.integrations.username`

  
  
Slack

|

  * `spec.integrations.apiTokenRef.name`

  * `spec.integrations.apiTokenRef.namespace`

  
  
VictorOps

|

  * `spec.integrations.apiKeyRef.name`

  * `spec.integrations.routingKeyRef.name`

  * `spec.integrations.routingKeyRef.namespace`

  
  
Webhook Settings

|

  * `spec.integrations.secretRef.name`

  * `spec.integrations.secretRef.namespace`

  * `spec.integrations.url`

  
  
`spec.integrations.accountId`

    

 _Type_ : string

 _Conditional_

Unique string that identifies your New Relic account. If you want to integrate
with New Relic, you must specify this setting.

`spec.integrations.apiKeyRef.name`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies your API key for Datadog, Opsgenie, or
VictorOps. If you want to integrate with Datadog, Opsgenie, or VictorOps, you
must specify this setting.

`spec.integrations.apiKeyRef.namespace`

    

 _Type_ : string

 _Conditional_

Namespace that contains your API key for Datadog, Opsgenie, or VictorOps. If
you want to integrate with Datadog, Opsgenie, or VictorOps, you must specify
this setting.

`spec.integrations.apiTokenRef.name`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies your API token for Slack or Flowdock. If
you want to integrate with Slack or Flowdock, you must specify this setting.

`spec.integrations.apiTokenRef.namespace`

    

 _Type_ : string

 _Conditional_

Namespace that contains your API token or Slack or Flowdock. If you want to
integrate with Slack or Flowdock, you must specify this setting.

`spec.integrations.enabled`

    

 _Type_ : boolean

 _Conditional_

Flag that indicates whether your cluster has Prometheus enabled. If you want
to integrate with Prometheus, you must specify this setting as `true`.

`spec.integrations.flowName`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies your Flowdock flow. If you want to
integrate with Flowdock, you must specify this setting.

`spec.integrations.licenseKeyRef.name`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies your license key for New Relic. If you
want to integrate with New Relic, you must specify this setting.

`spec.integrations.licenseKeyRef.namespace`

    

 _Type_ : string

 _Conditional_

Namespace that contains your license key for New Relic. If you want to
integrate with New Relic, you must specify this setting.

`spec.integrations.microsoftTeamsWebhookURL`

    

 _Type_ : string

 _Conditional_

String that specifies your Microsoft Teams incoming webhook URL. If you want
to integrate with Mircosoft Teams, you must specify this setting.

`spec.integrations.orgName`

    

 _Type:_ string

 _Conditional_

Human-readable string that identifies your Flowdock organization. If you want
to integrate with Flowdock, you must specify this setting.

`spec.integrations.passwordRef.name`

    

 _Type:_ string

 _Conditional_

Human-readable label that identifies your Prometheus password. If you want to
integrate with Prometheus, you must specify this setting.

`spec.integrations.passwordRef.namespace`

    

 _Type:_ string

 _Conditional_

Namespace that contains your Prometheus password. If you want to integrate
with Prometheus, you must specify this setting.

`spec.integrations.readTokenRef.name`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies your Insights Query Key for New Relic. If
you want to integrate with New Relic, you must specify this setting.

`spec.integrations.readTokenRef.namespace`

    

 _Type_ : string

 _Conditional_

Namespace that contains your Insights Query Key for New Relic. If you want to
integrate with New Relic, you must specify this setting.

`spec.integrations.region`

    

 _Type_ : string

 _Conditional_

 _Default_ : `US`

String value that indicates the API URL to use for Datadog or Opsgenie. If you
want to integrate with Datadog or Opsgenie, you must specify this setting.

Values for Opsgenie include `US` or `EU`.

Atlas supports the following Datadog regions in the Atlas Administration API:

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

`spec.integrations.routingKeyRef.name`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies your routing key for VictorOps. If you
want to integrate with VictorOps, you must specify this setting.

`spec.integrations.routingKeyRef.namespace`

    

 _Type_ : string

 _Conditional_

Namespace that contains your routing key for VictorOps. If you want to
integrate with VictorOps, you must specify this setting.

`spec.integrations.secretRef.name`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies your Webhook secret. If you want to
integrate with Webhook Settings, you must specify this setting.

`spec.integrations.secretRef.namespace`

    

 _Type_ : string

 _Conditional_

Namespace that contains your Webhook secret. If you want to integrate with
Webhook Settings, you must specify this setting.

`spec.integrations.scheme`

    

 _Type_ : string

 _Conditional_

String that indicates the Prometheus protocol scheme configured for requests.
Values include `http` or `https`. If you want to integrate with Prometheus,
you must specify this setting.

`spec.integrations.serviceDiscovery`

    

 _Type_ : string

 _Conditional_

Human-readable label that indicates the Prometheus service discovery method to
use. Values include `file` or `http`. If you want to integrate with
Prometheus, you must specify this setting.

`spec.integrations.serviceKeyRef.name`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies your service key for PagerDuty. If you
want to integrate with PagerDuty, you must specify this setting.

`spec.integrations.serviceKeyRef.namespace`

    

 _Type_ : string

 _Conditional_

Namespace that contains your service key for PagerDuty. If you want to
integrate with PagerDuty, you must specify this setting.

`spec.integrations.type`

    

 _Type_ : string

 _Conditional_

String value that indicates the third-party service to integrate with Atlas.
Values include:

  * `DATADOG`

  * `FLOWDOCK`

  * `MICROSOFT_TEAMS`

  * `NEW_RELIC`

  * `OPS_GENIE`

  * `PAGER_DUTY`

  * `PROMETHEUS`

  * `SLACK`

  * `VICTOR_OPS`

  * `WEBHOOK`

If you want to integrate with a third-party service, you must specify this
setting.

`spec.integrations.url`

    

 _Type_ : string

 _Conditional_

String that specifies your Webhook URL. If you want to integrate with Webhook
Settings, you must specify this setting.

`spec.integrations.username`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies the Prometheus user. If you want to
integrate with Prometheus, you must specify this setting.

`spec.integrations.writeTokenRef.name`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies your write token for New Relic. If you
want to integrate with New Relic, you must specify this setting.

`spec.integrations.writeTokenRef.namespace`

    

 _Type_ : string

 _Conditional_

Namespace that contains your write token for New Relic. If you want to
integrate with New Relic, you must specify this setting.

`spec.maintenanceWindow`

    

 _Type_ : object

 _Optional_

List that contains your maintenance window settings. You can specify the
following body parameters:

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
dayOfWeek

|

number

|

Required

|

Day of the week that you want the maintenance window to start, as a 1-based
integer.

|

Day of Week

|

Integer  
  
|  
  
Sunday

|

 **1**  
  
Monday

|

 **2**  
  
Tuesday

|

 **3**  
  
Wednesday

|

 **4**  
  
Thursday

|

 **5**  
  
Friday

|

 **6**  
  
Saturday

|

 **7**  
  
hourOfDay

|

number

|

Required

|

Hour of the day that you want the maintenance window to start. This parameter
uses the 24-hour clock, where midnight is **0** and noon is **12**.  
  
autoDeferOnceEnabled

|

boolean

|

Optional

|

Flag that indicates whether you want to defer all maintenance windows one week
they would be triggered.  
  
## Important

### Maintenance Window Considerations

Urgent Maintenance Activities

    Urgent maintenance activities such as security patches cannot wait for your chosen window. Atlas will start those maintenance activities when needed.
Ongoing Maintenance Operations

    Once maintenance is scheduled for your cluster, you cannot change your maintenance window until the current maintenance efforts have completed.
Maintenance Requires Replica Set Elections

    Atlas performs maintenance the same way as the maintenance procedure described in the MongoDB Manual. This procedure requires at least one replica set election during the maintenance window per replica set.
Maintenance Starts As Close to the Hour As Possible

    Maintenance always begins as close to the scheduled hour as possible, but in-progress cluster updates or unexpected system issues could delay the start time.

`spec.maintenanceWindow.autoDefer`

    

 _Type_ : boolean

 _Conditional_

Flag that indicates whether Atlas should defer all maintenance windows for one
week after you enable them.

`spec.maintenanceWindow.defer`

    

 _Type_ : boolean

 _Conditional_

Flag that indicates whether Atlas should defer scheduled maintenance. You must
schedule maintenance before you can successfully defer maintenance.
`spec.maintenanceWindow.defer` and `spec.maintenanceWindow.startASAP` can't
both be set to `true` at the same time.

## Important

While `spec.maintenanceWindow.defer` is set to `true`, Atlas Kubernetes
Operator defers scheduled maintenance every time you apply changes to the
`AtlasProject` custom resource. If you set `spec.maintenanceWindow.defer` to
`true`, you should change `spec.maintenanceWindow.defer` to `false` after you
apply changes.

`spec.maintenanceWindow.dayOfWeek`

    

 _Type_ : number

 _Conditional_

One-based integer that represents the day of the week that the maintenance
window starts. Use the following table to find the integer that corresponds to
each day:

Day of Week

|

Integer  
  
|  
  
Sunday

|

 **1**  
  
Monday

|

 **2**  
  
Tuesday

|

 **3**  
  
Wednesday

|

 **4**  
  
Thursday

|

 **5**  
  
Friday

|

 **6**  
  
Saturday

|

 **7**  
  
If you want to configure the maintenance window for your project, you must
specify this setting.

`spec.maintenanceWindow.hourOfDay`

    

 _Type_ : number

 _Conditional_

Zero-based integer that represents the hour of the of the day that the
maintenance window starts according to a 24-hour clock. Use `0` for midnight
and `12` for noon. If you want to configure the maintenance window for your
project, you must specify this setting.

`spec.maintenanceWindow.startASAP`

    

 _Type_ : boolean

 _Conditional_

Flag that indicates whether Atlas should immediately start maintenance.
`spec.maintenanceWindow.defer` and `spec.maintenanceWindow.startASAP` can't
both be set to `true` at the same time.

## Important

While `spec.maintenanceWindow.startASAP` is set to `true`, Atlas Kubernetes
Operator starts maintenance every time you apply changes to the `AtlasProject`
custom resource. If you set `spec.maintenanceWindow.startASAP` to `true`, you
should change `spec.maintenanceWindow.startASAP` to `false` after you apply
changes.

`spec.networkPeers`

    

 _Type_ : array

 _Optional_

List that contains the network peering configurations for the project.

`spec.projectIpAccessList`

    

 _Type_ : array

 _Required_

IP access list that grants network access to Atlas clusters in the project.
You can specify the following body parameters:

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
awsSecurityGroup

|

string

|

Conditional

|

Unique identifier of the AWS security group to add to the access list.

Your access list entry can include only one **awsSecurityGroup** , one
**cidrBlock** , or one **ipAddress**.

## Note

You must configure VPC peering for your project before you can add an AWS
security group to an access list.  
  
cidrBlock

|

string

|

Conditional

|

Range of IP addresses in CIDR notation to be added to the access list.

Your access list entry can include only one **awsSecurityGroup** , one
**cidrBlock** , or one **ipAddress**.  
  
comment

|

string

|

Optional

|

Comment associated with the access list entry.  
  
deleteAfterDate

|

date

|

Optional

|

Timestamp in ISO 8601 date and time format in UTC after which Atlas removes
the entry from the access list. The specified date must be in the future and
within one week of the time you make the API request.

## Important

You cannot set AWS security groups as temporary access list entries.

## Note

You may include an ISO 8601 time zone designator to ensure that the expiration
date occurs with respect to the local time in the specified time zone.  
  
ipAddress

|

string

|

Conditional

|

Single IP address to be added to the access list. Mutually exclusive with
**awsSecurityGroup** and **cidrBlock**.

Your access list entry can include only one **awsSecurityGroup** , one
**cidrBlock** , or one **ipAddress**.  
  
`spec.settings`

    

 _Type_ : object

 _Optional_

List that contains your project settings.

`spec.settings.IsCollectDatabaseSpecificsStatisticsEnabled`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether your project has collection of database statistics
in cluster metrics enabled.

`spec.settings.IsDataExplorerEnabled`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether your project has data explorer enabled.

`spec.settings.IsPerformanceAdvisorEnabled`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether your project has Performance Advisor enabled.

`spec.settings.IsRealtimePerformancePanelEnabled`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether your project has Realtime Performance Panel
enabled.

`spec.settings.IsSchemaAdvisorEnabled`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether your project has Schema Advisor enabled.

`spec.privateEndpoints`

    

 _Type_ : array

 _Optional_

List that contains the private endpoint configurations for the project.

`spec.teams`

    

 _Type_ : object

 _Optional_

Object that contains your team specifications. To learn more, see Configure
Teams.

`spec.teams.teamRef.name`

    

 _Type_ : string

 _Conditional_

Human-readable label from the `AtlasTeam` Custom Resource in the
`metadata.name` field. If you want to assign a team to this project, you must
specify this setting.

`spec.teams.teamRef.namespace`

    

 _Type_ : string

 _Conditional_

Namespace specified in the `AtlasTeam` Custom Resource if other than
`default`.

`spec.teams.teamRef.roles`

    

 _Type_ : string

 _Conditional_

Atlas User Roles that a team uses for this project. If you want to assign a
team to this project, you must specify this setting.

`spec.withDefaultAlertsSettings`

    

 _Type_ : boolean

 _Optional_

 _Default_ : `true`

Flag that indicates whether Atlas Kubernetes Operator creates a project with
the default alert configurations. If omitted, defaults to `true`.

If you use this setting, you must also set
`spec.alertConfigurationSyncEnabled` to `true` for Atlas Kubernetes Operator
to modify project alert configurations.

If you set this parameter to `false` when you create a project, Atlas doesn't
add the default alert configurations to your project.

This setting has no effect on existing projects.

For information on how this setting interacts with
`spec.alertConfigurationSyncEnabled`, see the Considerations.

`spec.X509CertRef.name`

    

 _Type_ : string

 _Optional_

Human-readable label that identifies the secret for the X.509 certificate.

← Custom Resources`AtlasDeployment` Custom Resource →

