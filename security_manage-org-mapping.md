Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Organization Mapping for Federated Authentication

Share Feedback

On this page

  * Prerequisites
  * Federation Management Access
  * Map an Organization to your Identity Provider
  * Change an Organization's Mapped Identity Provider
  *  _(Optional)_ Configure Advanced Options for Your Organization
  * Disconnect an Organization from the Federation Application

When you map organizations to your Identity Provider, Atlas grants users who
authenticate through the IdP membership in the selected organizations. You can
give these users a default role in the mapped organizations. Organization
mapping lets you configure a single IdP to grant users access to multiple
Atlas organizations.

You can apply the same IdP to multiple organizations. You can assign each
organization a single IdP.

## Prerequisites

To complete this tutorial, you must have already linked an IdP to Atlas and
mapped one or more domains to that IdP. For instructions on these procedures,
see:

  * Manage Identity Providers

  * Manage Domain Mapping for Federated Authentication

## Federation Management Access

You can manage federated authentication from the Federation Management
Console. You can access the console as long as you are an `Organization Owner`
in one or more organizations that are delegating federation settings to the
instance.

## Map an Organization to your Identity Provider

## Note

Atlas creates an `Organization's IdP certificate is about to expire` alert
automatically when you map an organization to an IdP provider. If you remove
the mapping, Atlas deletes all instances of this alert.

1

### Open the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

2

### Connect an organization to the Federation Application.

  1. Click View Organizations.

Atlas displays all organizations where you are an `Organization Owner`.

Organizations which are not already connected to the Federation Application
have Connect button in the Actions column.

  2. Click the desired organization's Connect button.

3

### Apply an Identity Provider to the organization.

From the Organizations screen in the management console:

  1. Click the Name of the organization you want to map to an IdP.

  2. On the Identity Provider screen, click Apply Identity Provider.

Atlas directs you to the Identity Providers screen which shows all IdPs you
have linked to Atlas.

  3. For the IdP you want to apply to the organization, click Add Organizations.

  4. In the Apply Identity Provider to Organizations modal, select the organizations to which this IdP applies.

  5. Click Confirm.

4

### Connect an organization to the Federation Application.

  1. Click Organizations in the left navigation.

  2. In the list of Organizations, ensure that your desired organization(s) now have the expected Identity Provider.

## Change an Organization's Mapped Identity Provider

Reconfigure your IdP to change the organizations to which it's mapped.

1

### Unmap the current Identity Provider.

  1. Click Organizations in the left navigation.

  2. Click the Identity Provider of the organization whose IdP you wish to change.

  3. Click Modify for the IdP which is currently mapped to the organization.

  4. At the bottom of the Edit Identity Provider form, deselect the organization.

  5. Click Next.

  6. Click Finish.

2

### Map the new Identity Provider.

  1. Click Modify for the IdP you want to map to the organization.

  2. At the bottom of the Edit Identity Provider form, select the organization.

  3. Click Next.

  4. Click Finish.

##  _(Optional)_ Configure Advanced Options for Your Organization

The following optional settings provide even greater control over user
management and authentication in your organization.

### Assign a Default User Role for Your Organization

You can assign users who authenticate through the IdP a default role in a
mapped organization. Configuring this option ensures that users who
authenticate through your IdP have the same set of permissions. This setting
is not required for organization mapping.

For instructions on assigning a default role, see Assign a Default User Role
for an Organization.

## Note

The selected default role only applies to users who authenticate through the
IdP if they do not have an Atlas role mapped to the IdP group already.

### Restrict Access to an Organization by Domain

You can restrict access to your organization to an approved list of domains.
This allows you to set the domains from which organization users can login
without needing to directly map those domains to your IdP.

For instructions on restricting access by domain, see Restrict Access to an
Organization by Domain.

## Disconnect an Organization from the Federation Application

When you disconnect an organization from the Federation Application, Atlas no
longer grants membership or a default organization role to users who
authenticate through the IdP.

From the Federation Management Console:

1

### Click View Organizations.

2

### Open the Actions dropdown for the organization you want to disconnect.

3

### Click Disconnect.

4

### Click Confirm.

← Manage Domain Mapping for Federated AuthenticationManage Mapping Atlas Roles
to IdP Groups →

