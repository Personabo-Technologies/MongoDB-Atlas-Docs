Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Organization Settings

Share Feedback

On this page

  * Live Migration: Connect to Atlas
  * Integrations

## Note

### Required Permissions

To perform any of the following actions, you must have the `Organization
Owner` role.

## Live Migration: Connect to Atlas

You connect to an organization in Atlas when you live migrate your deployment
from Cloud Manager or Ops Manager to Atlas.

## Integrations

You can configure Atlas for the following integrations:

  * Slack

  * Vercel

### Configure Slack Workspaces

1

#### Navigate to the Integrations page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Integrations in the sidebar.

2

#### Click Add to Slack.

3

#### Sign in to your Workspace.

  1. Type your workspace name into the field.

  2. Click Continue.

  3. Select your authentication method.

  4. Click Authorize.

4

#### Click Save.

## Important

You can authorize only one Slack Workspace for each Organization.

### Select Organization to Remove Slack Authorization

1

#### Navigate to the Integrations page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Integrations in the sidebar.

2

#### Click Remove Integration.

## Important

This does not stop Atlas from sending alerts. To stop Atlas from sending
alerts to Slack, you must delete the Slack alert setting.

### Configure Vercel Integrations

You can connect your Atlas clusters to applications that you deploy using
Vercel. To learn more, see Integrate with Vercel.

← Manage Organization TeamsManage Project Access →

