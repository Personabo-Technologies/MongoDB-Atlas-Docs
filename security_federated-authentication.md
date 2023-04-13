Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Federated Authentication

Share Feedback

On this page

  * Federation Management Access
  * Quick Start
  * Tutorials
  * Consideration for Restricted Access to Atlas UI
  * Consideration for Two-Factor Authentication

MongoDB Federated Authentication links your credentials across many MongoDB
systems. Atlas implements authentication using the Federated Identity
Management model.

Using the FIM model:

  * Your company manages your credentials using an Identity Provider (IdP). With its IdP, your company can enable you to authenticate with other services across the web.

  * You configure MongoDB Atlas to authenticate using data passed from your IdP.

This goes beyond SSO as your IdP manages your credentials, not MongoDB. Your
users can use Atlas without needing to remember another username and password.

## Important

While you have a federated IdP enabled, Atlas disables any other
authentication mechanisms.

click to enlarge

To link your IdP to Atlas you provide each with the appropriate metadata.
After you link your IdP to Atlas, map domains, organizations, and roles to
your IdP:

Domain Mapping

    Atlas routes users with email addresses that use mapped domains to the associated IdP.
Organization Mapping

    Atlas grants users who log in through the IdP access to mapped Atlas organizations.
Role Mapping

    As part of the organization mapping, you can choose which role to grant your users. These roles map to groups in your IdP.

## Federation Management Access

You can manage federated authentication from the Federation Management
Console. You can access the console as long as you are an `Organization Owner`
in one or more organizations that are delegating federation settings to the
instance.

To open the Federation Management console:

1

### Navigate to the Settings page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click the Organization Settings icon next to the Organizations menu.

2

### Navigate to the Federation Management App.

In the Setup Federated Login or Manage Federation Settings section, click
Visit Federation Management App.

## Quick Start

If you're configuring single sign-on for users in your organization for the
first time, you can follow MongoDB's federation management Quick Start Guide.

To configure single sign-on with the Quick Start Guide:

1

### Navigate to the Federation Management App.

If it is not already displayed, open the Overview page using the left
navigation panel.

2

### Click Begin on the Quick Start Guide card.

The Quick Start Guide walks you through the following:

  1. Adding and verifying your domains.

  2. Configuring your IdP with Atlas.

  3. Connecting your domains to your IdP.

  4. Activating your IdP for users to access MongoDB.

Complete each of the four steps in order.

## Note

If you've already completed the federation management Quick Start but want to
go through those steps again, click the link at the bottom of the Federation
Management console Overview page.

## Tutorials

To configure federated authentication from the Federation Management console
in Atlas, you must:

  1. Click Manage Identity Providers and Link an Identity Provider to Atlas to ensure that your users are authenticated through your trusted IdP.

  2. Click Manage Domains and Map Domains to your Identity Provider to simplify the login experience for users from specified domains. Atlas authenticates users through a mapped IdP if their email address matches a mapped domain.

After federating authentication, you can simplify user authorization. In the
Federation Management console, click Manage Organizations. You can perform
these activities:

  1. Map Atlas organizations to your IdP.

  2. Map Atlas roles to groups in your IdP.

End-to-end tutorials on implementing federated authentication:

  * Azure AD

  * Google Workspace

  * Okta

## Consideration for Restricted Access to Atlas UI

If you enable IP access list for the Atlas UI for an organization, and
restrict access by any user to at least one federated organization, Atlas
doesn't allow this user to access the Federation Management console.

## Consideration for Two-Factor Authentication

Atlas bypasses 2FA for users who authenticate with federated authentication
through your IdP. If a user authenticates through your IdP and has 2FA for
their Atlas account enabled, Atlas doesn't prompt the user for 2FA. Instead,
you can configure your trusted IdP to prompt users for 2FA. To learn more, see
Manage Your Multi-Factor Authentication Options.

← Atlas UI AuthenticationManage Identity Providers →

