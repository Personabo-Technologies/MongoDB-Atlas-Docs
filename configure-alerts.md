Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Alert Settings

Share Feedback

On this page

  * Default Alert Settings
  * Default Alert Settings
  * Notification Options
  * Configure an Alert
  * Configure a Maintenance Window Alert
  * View Alert Configurations
  * Disable an Alert
  * Enable an Alert
  * Delete an Alert

For each organization and project, you can select which conditions trigger
alerts and how users are notified.

## Note

`M0` free clusters and `M2/M5` shared clusters only trigger alerts related to
the metrics supported by those clusters. See Atlas M0 (Free Cluster), M2, and
M5 Limitations for complete documentation on `M0/M2/M5` alert and metric
limitations.

Organization Alerts

Project Alerts

Organization Alerts

Project Alerts

## Important

### Required Privileges

To manage all organization alerts, you must have the `Organization Owner` role
for the organization.

The `Organization Billing Admin` role grants a limited authorization to manage
billing alerts.

## Default Alert Settings

Atlas provides no default alerts for organizations.

## Notification Options

Organization Alerts

Project Alerts

When you configure an alert, you select how notifications are sent. You can
select multiple notification methods, such as email, text message, or team
collaboration tools.

Atlas supports Slack as a notification method. From the organization's
Settings menu, click Add to Slack in Slack Settings and log in to your
preferred Slack workspace.

Atlas supports configuring all of the following notification methods during
alert configuration:

  * Atlas Organization

  * Atlas User

  * Email

  * SMS

  * PagerDuty

  * Flowdock

  * Datadog

  * VictorOps

  * Opsgenie

  * Microsoft Teams

## Configure an Alert

When you create a new alert, you can clone an existing alert. You can also
update an existing alert configuration.

Organization Alerts

Project Alerts

1

### Navigate to the Alerts page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Alerts in the sidebar.

2

### Choose whether to create a new alert setting, clone an existing alert
setting, or update an existing alert setting.

To create a new alert:

  1. Click Add Alert.

To clone an existing alert setting:

  1. Click the Alert Settings tab.

  2. Locate the alert setting you want to clone.

  3. Click __then Clone in that alert setting's row.

To update an existing alert setting:

  1. Click the Alert Settings tab.

  2. Locate the alert setting you want to update.

  3. Click __then Edit in that alert setting's row.

3

### Choose the Target.

Click User or Billing under Select a Target.

4

### Choose the Condition.

Under Select a Condition:

  * If you chose User, select:

    * `User(s) in the organization do not have 2FA enabled`

    * `User has joined the organization`

    * `User has left the organization`

    * `User's role has been changed`

  * If you chose Billing:

    1. Select from the following options:

      * `Credit card is about to expire`

      * `Amount billed yesterday is above`

      * `Current bill for any single project is above`

      * `Current bill for the organization is above`

    2. If above $ appears next to the option you selected, specify the amount in USD where Atlas should trigger the alert if the selected condition exceeds that value.

5

### Select the Notification Method.

Under the Add Notification Method heading, click the button for the particular
notification method you want to use.

Notification Option

|

User Alerts

|

Billing Alerts

|

Description  
  
|||  
  
Atlas Organization

|

 __

|

 __

|

Sends the alert by email or text message to users with specific roles in the
Organization.

  1. Select the Organization roles that should receive the alerts from the Select Role(s) check boxes or select All Roles for all users in the Organization to receive the alert.

  2. Select SMS to send these alerts to the mobile number configured for each Atlas Organization user in their Account page.

  3. Select Email to send these alerts to the email address configured for each Atlas Organization user in their Account page. Email is checked by default.

  
  
Atlas User

|

 __

|

 __

|

Sends the alert by email or text message to a specified Atlas user.

  1. Select SMS to send these alerts to the mobile number configured for the Atlas user in their Account page.

  2. Select Email to send these alerts to the email address configured for the Atlas user in their Account page. Email is checked by default.

  
  
Email

|

 __

|

 __

|

Sends the alert to any email address you provide.  
  
Mobile Number

|

 __

|

 __

|

Sends the alert to a mobile number. Atlas removes all punctuation and letters
and uses only the digits. If you are outside of the United States or Canada,
include`011` and the country code because Atlas uses the U.S.-based Twilio to
send text messages. As an alternative to your non-U.S. telephone number, use a
Google Voice telephone number.

## Example

For New Zealand enter `01164` before the phone number.  
  
Slack

|

 __

|

 __

|

Sends the alert to a Slack channel in the authorized Slack workplace for the
Organization. To learn more about Slack authorization, seeAuthorize Slack to
Receive Organization Alerts. Enter the channel name.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
Flowdock

|

 __

|

 __

|

Sends the alert to a Flowdock account. Enter the following:

Org Name:

    The Flowdock organization name in lower-case letters. This is the name that appears after `www.flowdock.com/app/` in the URL string.
Flow Name:

    

The flow name in lower-case letters. The flow name appears after the
organization name in the URL string:

`www.flowdock.com/app/<organization-name>/<flow-name>`

User API Token:

    Your Flowdock personal API token found on the https://www.flowdock.com/account/tokens page of your Flowdock account.  
  
PagerDuty

|

|

 __

|

Sends the alert to a PagerDuty account. Enter only the PagerDuty service key.
Define escalation rules and alert assignments directly in PagerDuty.

Acknowledge PagerDuty alerts from the PagerDuty dashboard.

## Note

All new PagerDuty keys use their Events API v2.

If you have an Events API v1 key, you can continue to use that key with Atlas.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
Datadog

|

 __

|

 __

|

Sends the alert to a Datadog account as a Datadog event.

When the alert is first opened, Atlas sends the alert as an "error" event.
Subsequent updates are sent as "info" events. When the alert is closed, Atlas
sends a "success" event.

  1. Enter your DataDog API key under API Key and click Validate Datadog API Key.

  2. Enter your API region.

Atlas supports the following Datadog regions in the Atlas UI:

    * `US1`

    * `US3`

    * `US5`

    * `EU1`

Datadog uses `US1` by default.

To learn more about Datadog's regions, see Datadog Sites.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
VictorOps

|

|

 __

|

Sends the alert to a VictorOps account.

Enter the alphanumeric API key from VictorOps to integrate the VictorOps
endpoint for alerts. Add dashes to the API key so it matches the format
`xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`. For example,
`489f7he7-790b-9896-a8cf-j4757def1161`. Enter an optional routing key to route
alerts to a specific VictorOps group. Click Post Test Alert to test the
VictorOps configuration. Define escalation and routing rules directly in
VictorOps.

This option is available only for alerts that you must acknowledge.
Informational alerts like an Atlas user has joined the organization can't use
this notification method.

Acknowledge VictorOps alerts from the VictorOps dashboard.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
Opsgenie

|

|

 __

|

Sends the alert to an Opsgenie account. Enter only the Opsgenie API key from
an Opsgenie REST API integration. Define escalation rules and alert
assignments in Opsgenie.

This option is available only for alerts that you must acknowledge.
Informational alerts like an Atlas user has joined the organization can't use
this notification method.

Acknowledge Opsgenie alerts from the Opsgenie dashboard.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
Microsoft Teams

|

 __

|

 __

|

Sends the alert to a Microsoft Teams channel. You can view these alerts in the
Adaptive Card displayed in your channel.

To send alert notifications to a Microsoft Teams channel, you must create a
Microsoft Teams incoming webhook. After creating the webhook, you can use the
automatically generated URL to configure your Microsoft Teams integration in
Atlas.

To setup the integration, see Integrate with Microsoft Teams.

## Note

When you view or edit the alert for a Microsoft Teams notification, the URL
appears partially redacted.  
  
6

### Click Save.

## Configure a Maintenance Window Alert

You can configure Maintenance Window Alerts for projects with configured
maintenance windows.

1

### Navigate to the Alerts page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click the __ Project Alerts icon in the navigation bar, or click Alerts in the sidebar.

2

### Click Alert Settings.

3

### Select the maintenance window alerts you want to configure.

You can configure the following maintenance window alerts:

  * `Maintenance Is Scheduled`

  * `Maintenance Started`

  * `Maintenance No Longer Needed`

For the alert you want to configure, click __then Edit in that alert setting's
row.

4

### Select the alert recipients and delivery methods.

In the Send to section, click Add and select from the options described in the
following table.

Notification Option

|

Description  
  
|  
  
Atlas Project

|

Sends the alert by email or text message to users with specific roles in the
Project.

## Note

Atlas Project is the default alert recipient. You can configure the roles the
alert is sent to and how it's delivered. You can't add a second Atlas Project
as the recipient.

Atlas Project is available as an option in the Add list only if it is not
currently in the recipients list.

  1. Select the Project roles that should receive the alerts from the Select Role(s) check boxes or select All Roles for all users in the Project to receive the alert.

  2. Select SMS to send these alerts to the mobile number configured for each Atlas Project user in their Account page.

  3. Select Email to send these alerts to the email address configured for each Atlas Project user in their Account page. Email is checked by default.

  
  
Atlas Organization

|

Sends the alert by email or text message to users with specific roles in the
Organization.

  1. Select the Organization roles that should receive the alerts from the Select Role(s) check boxes or select All Roles for all users in the Organization to receive the alert.

  2. Select SMS to send these alerts to the mobile number configured for each Atlas Organization user in Account page.

  3. Select Email to send these alerts to the email address configured for each Atlas Organization user in Account page. Email is checked by default.

  
  
Atlas User

|

Sends the alert by email or text message to a specified Atlas user.

  1. Select SMS to send these alerts to the mobile number configured for the Atlas user in their Account page.

  2. Select Email to send these alerts to the email address configured for the Atlas user in their Account page. Email is checked by default.

  
  
Email

|

Sends the alert to an email address.  
  
SMS

|

Sends the alert to a mobile number. Atlas removes all punctuation and letters
and uses only the digits. If you are outside of the United States or Canada,
include `011` and the country code because Atlas uses the U.S.-based Twilio to
send text messages. As an alternative to your non-U.S. telephone number, use a
Google Voice telephone number.

## Example

For New Zealand enter `01164` before the phone number.  
  
Slack

|

Sends the alert to a Slack channel. Enter the channel name and either an API
token or a Bot token. To create an API token, see the
https://api.slack.com/web page in your Slack account. To learn more about Bot
users in Slack, see https://api.slack.com/bot-users.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
Flowdock

|

Sends the alert to a Flowdock account. Enter the following:

Org Name:

    The Flowdock organization name in lower-case letters. This is the name that appears after `www.flowdock.com/app/` in the URL string.
Flow Name:

    

The flow name in lower-case letters. The flow name appears after the
organization name in the URL string:

`www.flowdock.com/app/<organization-name>/<flow-name>`

User API Token:

    Your Flowdock personal API token found on the https://www.flowdock.com/account/tokens page of your Flowdock account.  
  
Webhook

|

Sends an HTTP POST request to an endpoint for programmatic processing. The
request body contains a JSON document that uses the same format as the Atlas
Administration API Alerts resource.

This option is available only if you have configured Webhook settings on the
Integrations page.

## Note

When you view or edit the alert for a webhook notification, the URL appears
partially redacted, and the secret appears completely redacted.

  1. In the Webhook URL field, specify the target URL for webhook-based alerts.

  2. (Optional) If you set up your Webhook integration with a secret, in the Webhook Secret field, specify the authentication secret for webhook-based alerts.

  
  
Datadog

|

Sends the alert to a Datadog account as a Datadog event.

When the alert is first opened, Atlas sends the alert as an "error" event.
Subsequent updates are sent as "info" events. When the alert is closed, Atlas
sends a "success" event.

  1. Enter your DataDog API key under API Key and click Validate Datadog API Key.

  2. Enter your API region.

Atlas supports the following Datadog regions in the Atlas UI:

    * `US1`

    * `US3`

    * `US5`

    * `EU1`

Datadog uses `US1` by default.

To learn more about Datadog's regions, see Datadog Sites.

## Note

After you create a notification which requires an API or integration key, the
key appears partially redacted when you:

  * View or edit the alert through the Atlas UI.

  * Query the alert for the notification through the Atlas Administration API.

  
  
Microsoft Teams

|

Sends the alert to a Microsoft Teams channel as an Adaptive Card.

To send alert notifications to a Microsoft Teams channel, you must create a
Microsoft Teams incoming webhook. After creating the webhook, you can use the
automatically generated URL to configure your Microsoft Teams integration in
Atlas.

To setup the integration, see Integrate with Microsoft Teams.

## Note

When you view or edit the alert for a Microsoft Teams notification, the URL
appears partially redacted.  
  
5

### Click Save.

## View Alert Configurations

Organization Alerts

Project Alerts

You can view all alerts, alert settings, and deleted alerts on the
Organization Alerts page. To learn more, see Alerts Workflow.

To view your alert configurations, navigate to the Alerts page for your
organization using the following steps:

1

If it is not already displayed, select your desired organization from the __
Organizations menu in the navigation bar.

2

### Click Alerts in the sidebar.

3

### Click the Alert Settings tab.

## Disable an Alert

Project Alerts

Atlas CLI

Atlas UI

To disable one alert configuration in the specified project using the Atlas
CLI, run the following command:

    
    
    atlas alerts settings disable <alertConfigId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas alerts settings disable.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Enable an Alert

To enable an alert that you previously disabled:

Organization Alerts

Project Alerts

1

### Navigate to the Alerts page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Alerts in the sidebar.

2

### Click Alert Settings.

3

### Re-enable the alert setting.

  1. On the row for a specific alert, click __.

  2. Click Enable.

## Delete an Alert

Project Alerts

## Warning

Don't delete the Maintenance Window Alerts that are created when you configure
a maintenance window.

If you delete a maintenance window alert, disable and then re-enable your
maintenance window to re-create the alerts.

You must have one of the following roles to delete an alert setting:

  * `Project Owner`

  * `Organization Owner`

Atlas CLI

Atlas UI

To delete one alert configuration in the specified project using the Atlas
CLI, run the following command:

    
    
    atlas alerts settings delete <alertConfigId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas alerts settings delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

If you delete an alert setting, Atlas cancels active alerts related to the
setting. A deleted alert setting does not remain visible.

← Review Alert ConditionsResolve Alerts →

