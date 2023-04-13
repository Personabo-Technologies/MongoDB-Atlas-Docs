Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Integrate with Microsoft Teams

Share Feedback

On this page

  * Prerequisites
  * Procedure

You can integrate Atlas with Microsoft Teams to receive Atlas alerts in your
Microsoft Teams channel.

## Prerequisites

To integrate Atlas with Microsoft Teams and receive alerts in your Microsoft
Teams channel, you must have a Microsoft Teams account.

## Procedure

To integrate Atlas with Microsoft Teams and receive alerts in your Microsoft
Teams channel:

Organization Alerts

Project Alerts

## Important

### Required Privileges

To manage all organization alerts, you must have the `Organization Owner` role
for the organization.

The `Organization Billing Admin` role grants a limited authorization to manage
billing alerts.

1

### Create the Microsoft Teams incoming webhook.

  1. Navigate to the Microsoft Teams channel where you want to add the webhook.

  2. Select __from the top navigation bar. A dropdown menu of available options displays.

  3. Select Connectors from the dropdown menu. A modal with available connectors displays.

  4. Search for Incoming Webhook and select Add. A modal with information about the Incoming Webhook connector displays.

  5. Click Add.

  6. Click Configure. A modal displays.

  7. In the modal, enter a name for your webhook. Optionally, you can upload a unique image to help you identify your webhook.

  8. Click Create.

  9. Copy the incoming webhook URL.

## Important

Atlas requires this URL to configure the integration.

  10. Click Done

2

### Navigate to the Alerts page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Alerts in the sidebar.

3

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

4

### Choose the Target.

Click User or Billing under Select a Target.

5

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

6

### Configure the Microsoft Teams integration.

  1. Under the Add Notification Method heading, click the button for Microsoft Teams.

  2. Enter the incoming webhook URL in the provided text box.

  3. To test the integration, click Post Test Alert.

  4. Under Recurrence, set the recurrence conditions in the provided text boxes.

  5. Click Add.

← Integrate with DatadogIntegrate with PagerDuty →

