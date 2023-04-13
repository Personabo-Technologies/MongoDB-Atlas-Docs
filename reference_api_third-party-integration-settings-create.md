Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Configuration for a Third-Party Service Integration

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
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

## Important

Each project can only have one configuration per `{INTEGRATION-TYPE}`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /groups/{GROUP-ID}/integrations/{INTEGRATION-TYPE}  
      
  
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
  
`{INTEGRATION-TYPE}`

|

Required

|

Third-party service identifier. Accepted values are:

  * `PAGER_DUTY`

  * `SLACK`

  * `DATADOG`

  * `NEW_RELIC`

  * `OPS_GENIE`

  * `VICTOR_OPS`

  * `FLOWDOCK`

  * `WEBHOOK`

  * `MICROSOFT_TEAMS`

  * `PROMETHEUS`

  
  
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

The request body should be a single integration view (i.e. a JSON
configuration object) for a single third-party service to add to the project.
Always include a `type` property equal to the third-party service
`INTEGRATION_TYPE`.

Service

|

Configuration Options  
  
|  
  
PagerDuty

|

You must provide the following fields when you configure a PagerDuty
integration:

|

Property

|

Description  
  
|  
  
`type`

|

`PAGER_DUTY`  
  
`serviceKey`

|

Your Service Key.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
Slack

|

## Important

### Slack integrations now use the OAuth2 verification method and must be
initially configured, or updated from a legacy integration, through the Atlas
third-party service integrations page.

Legacy tokens will soon no longer be supported.

You must provide the following fields when you reconfigure an existing Slack
integration:

|

Property

|

Description  
  
|  
  
`type`

|

`SLACK`  
  
`apiToken`

|

Your API Token.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
`teamName`

|

Your team name.  
  
You may also include the following fields:

Property

|

Description  
  
|  
  
`channelName`

|

The channel name to reconfigure.  
  
Datadog

|

You must provide the following fields when you configure a Datadog
integration:

|

Property

|

Description  
  
|  
  
`type`

|

`DATADOG`  
  
`apiKey`

|

Your API Key.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
`region`

|

Indicates the API URL to use.

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
  
New Relic

|

You must provide the following fields when you configure a New Relic
integration:

## Important

Effective Wednesday, June 16th, 2021, New Relic no longer supports the plugin-
based integration with MongoDB. We do not recommend that you sign up for the
plugin-based integration.

To learn more, see the New Relic Plugin EOL Statement. Consider configuring an
alternative monitoring integration before June 16th to maintain visibility
into your MongoDB deployments.

|

Property

|

Description  
  
|  
  
`type`

|

`NEW_RELIC`  
  
`licenseKey`

|

Your License Key.  
  
`accountId`

|

Unique identifier of your New Relic account.  
  
`writeToken`

|

Your Insights Insert Key.  
  
`readToken`

|

Your Insights Query Key.  
  
Opsgenie

|

You must provide the following fields when you configure a Opsgenie
integration:

|

Property

|

Description  
  
|  
  
`type`

|

`OPS_GENIE`  
  
`apiKey`

|

Your API Key.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
`region`

|

Indicates which API URL to use, either `US` or `EU`. Opsgenie will use `US` by
default.  
  
VictorOps

|

You must provide the following fields when you configure a VictorOps
integration:

|

Property

|

Description  
  
|  
  
`type`

|

`VICTOR_OPS`  
  
`apiKey`

|

Your API Key.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
You may also include the following fields:

Property

|

Description  
  
|  
  
`routingKey`

|

An optional field for your Routing Key.  
  
Flowdock

|

You must provide the following fields when you configure a Flowdock
integration:

|

Property

|

Description  
  
|  
  
`type`

|

`FLOWDOCK`  
  
`flowName`

|

Your Flowdock Flow name.  
  
`apiToken`

|

Your API Token.  
  
`orgName`

|

Your Flowdock organization name.  
  
Webhook Settings

|

You must provide the following fields when you configure webhook settings:

|

Property

|

Description  
  
|  
  
`type`

|

`WEBHOOK`  
  
`url`

|

Your webhook URL.  
  
You may also include the following fields:

Property

|

Description  
  
|  
  
`secret`

|

An optional field for your webhook secret.

## Note

When you view or edit the alert for a webhook notification, the URL appears
partially redacted, and the secret appears completely redacted.  
  
Microsoft Teams

|

You must provide the following fields when you configure a Microsoft Teams
integration:

|

Property

|

Description  
  
|  
  
`type`

|

`MICROSOFT_TEAMS`  
  
`microsoftTeamsWebhookUrl`

|

Your Microsoft Teams incoming webhook URL.

## Note

When you view or edit the alert for a Microsoft Teams notification, the URL
appears partially redacted.  
  
Prometheus

|

You must provide the following fields when you configure a Prometheus
integration:

|

Property

|

Description  
  
|  
  
`type`

|

`PROMETHEUS`  
  
`username`

|

Your Prometheus username.  
  
`password`

|

Your Prometheus password.  
  
`serviceDiscovery`

|

Indicates which Prometheus service discovery method is used, either `file` or
`http`.  
  
`enabled`

|

Whether your cluster has Prometheus enabled.  
  
## Response Elements

The response includes a `results` array which lists all third-party
integration configurations for the project as objects, and a `totalCount` of
the services integrated with the project. The `results` array includes the
integration view added by the request.

Each third-party integration configuration object includes a `type` property
equal to its own integration type (e.g. `"type": "PAGER_DUTY"` for the
PagerDuty service). Additionally, each third-party service configuration
object provides details specific to that service. The following lists the
properties returned for each third-party service configuration object:

Service

|

Result  
  
|  
  
PagerDuty

|

A returned PagerDuty integration configuration object will contain the
following fields:

|

Property

|

Description  
  
|  
  
`type`

|

`PAGER_DUTY`  
  
`serviceKey`

|

Your Service Key.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
Slack

|

A returned Slack integration configuration object will contain the following
fields:

|

Property

|

Description  
  
|  
  
`type`

|

`SLACK`  
  
`apiToken`

|

Your API Token.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
`teamName`

|

Your team name. This field may not be present with a legacy Slack integration.  
  
`channelName`

|

The configured Slack channel name. An empty string if the value is not set.  
  
Datadog

|

A returned Datadog integration configuration object will contain the following
fields:

|

Property

|

Description  
  
|  
  
`type`

|

`DATADOG`  
  
`apiKey`

|

Your API Key.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
`region`

|

Indicates the API URL to use.

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
  
New Relic

|

A returned New Relic integration configuration object will contain the
following fields:

## Important

Effective Wednesday, June 16th, 2021, New Relic no longer supports the plugin-
based integration with MongoDB. We do not recommend that you sign up for the
plugin-based integration.

To learn more, see the New Relic Plugin EOL Statement. Consider configuring an
alternative monitoring integration before June 16th to maintain visibility
into your MongoDB deployments.

|

Property

|

Description  
  
|  
  
`type`

|

`NEW_RELIC`  
  
`licenseKey`

|

Your License Key.  
  
`accountId`

|

Unique identifier of your New Relic account.  
  
`writeToken`

|

Your Insights Insert Key.  
  
`readToken`

|

Your Insights Query Key.  
  
Opsgenie

|

A returned Opsgenie integration configuration object will contain the
following fields:

|

Property

|

Description  
  
|  
  
`type`

|

`OPS_GENIE`  
  
`apiKey`

|

Your API Key.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
`region`

|

Indicates which API URL is used, either `US` or `EU`. Opsgenie will use `US`
by default.  
  
VictorOps

|

A returned VictorOps integration configuration object will contain the
following fields:

|

Property

|

Description  
  
|  
  
`type`

|

`VICTOR_OPS`  
  
`apiKey`

|

Your API Key.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
The configuration object may also contain the following fields, depending on
your configuration:

Property

|

Description  
  
|  
  
`routingKey`

|

An optional field returned if you have a Routing Key configured.  
  
Flowdock

|

A returned Flowdock integration configuration object will contain the
following fields:

|

Property

|

Description  
  
|  
  
`type`

|

`FLOWDOCK`  
  
`flowName`

|

Your Flowdock Flow name.  
  
`apiToken`

|

Your API Token.  
  
`orgName`

|

Your Flowdock organization name.  
  
Webhook Settings

|

A returned webhook configuration object will contain the following fields:

|

Property

|

Description  
  
|  
  
`type`

|

`WEBHOOK`  
  
`url`

|

Your webhook URL.  
  
The configuration object may also contain the following fields, depending on
your configuration:

Property

|

Description  
  
|  
  
`secret`

|

An optional field returned if your webhook is configured with a secret.

## Note

When you view or edit the alert for a webhook notification, the URL appears
partially redacted, and the secret appears completely redacted.  
  
Microsoft Teams

|

A returned Microsoft Teams configuration object will contain the following
fields:

|

Property

|

Description  
  
|  
  
`type`

|

`MICROSOFT_TEAMS`  
  
`microsoftTeamsWebhookUrl`

|

Your Microsoft Teams incoming webhook URL.

## Note

When you view or edit the alert for a Microsoft Teams notification, the URL
appears partially redacted.  
  
Prometheus

|

A returned Prometheus configuration object will contain the following fields:

|

Property

|

Description  
  
|  
  
`type`

|

`PROMETHEUS`  
  
`username`

|

Your Prometheus username.  
  
`serviceDiscovery`

|

Indicates which service discovery method is used, either `file` or `http`.  
  
`scheme`

|

Your Prometheus protocol scheme configured for requests.  
  
`enabled`

|

Whether your cluster has Prometheus enabled.  
  
## Example Request

    
    
    curl -X POST -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/5d791c84ff7a2522cc4f9aa1/integrations/FLOWDOCK" \  
      
    -H 'Content-Type: application/json' \  
    -d '{ "type": "FLOWDOCK", "flowName": "myFlowName", "apiToken": "1234567890", "orgName": "myOrg" }'  
  
## Example Response

    
    
    {  
      
         "links": [  
             {  
                 "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/5d791c84ff7a2522cc4f9aa1/integrations/FLOWDOCK?pageNum=1&itemsPerPage=100",  
                 "rel": "self"  
             }  
         ],  
         "results": [  
             {  
                 "apiKey": "******7890",  
                 "region": "US",  
                 "type": "DATADOG"  
             },  
             {  
                 "apiToken": "******7890",  
                 "channelName": "My Channel",  
                 "teamName": "My Team",  
                 "type": "SLACK"  
             },  
             {  
                 "apiToken": "1234567890",  
                 "flowName": "myFlowName",  
                 "orgName": "myOrg",  
                 "type": "FLOWDOCK"  
             }  
         ],  
         "totalCount": 3  
     }  
  
What is MongoDB Atlas? →

