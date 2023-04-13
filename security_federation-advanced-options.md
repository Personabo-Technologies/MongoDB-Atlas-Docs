Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Advanced Options for Federated Authentication

Share Feedback

On this page

  * Federation Management Access
  * Assign a Default User Role for an Organization
  * Restrict Access to an Organization by Domain
  * Bypass SAML Mode
  * Sign in After Enabling Bypass SAML Mode
  * Restrict User Membership to the Federation

You can configure advanced options in your Federated Authentication instance
for greater control over your federated users and authentication flow.

## Federation Management Access

You can manage federated authentication from the Federation Management
Console. You can access the console as long as you are an `Organization Owner`
in one or more organizations that are delegating federation settings to the
instance.

To open the Federation Management Console:

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

## Assign a Default User Role for an Organization

You can configure Atlas to automatically provision each user who authenticates
through the IdP with a default role in a mapped organization. You can select
different roles for different organizations.

## Note

The selected role only applies to users who authenticate through the IdP if
they do not already have a role in the organization.

1

### Click Organizations in the left navigation pane.

2

### Click the Name of the organization for which you want to assign default
permissions.

3

### In the Default User Role dropdown, select the desired role.

To remove a default user role, click the __next to the dropdown.

## Restrict Access to an Organization by Domain

You can specify a list of approved domains to prevent users outside of those
domains from accessing your organization. Use this list to define a list of
approved domains for your organization without needing to directly map those
domains to your IdP.

## Important

### Considerations

Once you enable the Restrict Access by Domain option:

  * You can only invite new users to join your organization whose email addresses are in the approved list of domains.

  * Users who are already in your organization whose usernames do not contain a domain in the approved list are _not_ restricted access to your organization.

  * Any domains which are mapped to your IdP are automatically added to the approved list.

From the Federation Management Console:

1

### Click Organizations in the left navigation pane.

2

### Click the Name of the organization for which you want to restrict access.

3

### In the Advanced Settings, toggle Restrict Access by Domain to On.

When you enable this setting, Atlas automatically adds all domains which are
mapped to an IdP to the list of Approved Domains.

4

### Add domains to the approved list.

To add domains to the approved list, you can either:

  1. Click Add Domains from Existing Members. Atlas opens a modal containing domains from existing user email addresses in your organization. Use this list to easily enable access for users who are already part of your organization.

Use the checkboxes to select the desired domains, then click Add to add them
to the approved list.

  2. Click Add Domains. Atlas opens a modal where you can manually add domains the approved list.

Enter the domain you want approve in the input box, then click Add. Repeat
this process for each domain you want to approve.

## Note

If you have restricted user membership to your federation, Atlas warns you if
you add a domain which is being used to access organizations outside of your
federation.

Once you have added all desired domains, click Submit.

## Bypass SAML Mode

Bypass SAML Mode provides a login URL which bypasses your federated
authentication, and instead allows you to authenticate with your Atlas
credentials.

If your Federated Authentication settings are not properly configured, you may
not be able to log in to Atlas through your IdP. The Bypass SAML Mode URL
helps prevent you from being locked out of your Atlas organization. While
configuring and testing your IdP, we recommend that you make note of the
Bypass SAML Mode URL to ensure you can log in to Atlas and properly configure
your Federated Authentication settings.

Each Bypass SAML Mode URL is associated with an individual IdP, and
corresponds to the IdP's Login URL.

Bypass SAML Mode is enabled by default, however you may want to disable it as
a security measure once you are confident that you have properly configured
your Federated Authentication.

To set Bypass SAML Mode, from the Federation Management Console:

1

### Click Identity Providers in the left navigation pane.

2

### Locate the IdP for which you want to view / modify the Bypass SAML Mode
setting.

3

### Toggle Bypass SAML Mode as desired.

4

### If you are disabling Bypass SAML Mode, click Disable in the confirmation
dialog.

## Sign in After Enabling Bypass SAML Mode

After you enable Bypass SAML Mode, you must sign in to Atlas using:

  * The Bypass SAML Mode URL for your IdP.

  * A username that:

    * Contains the domain you mapped to your IdP.

    * You have used to sign in to Atlas or Cloud Manager before you configured Federated Authentication.

## Restrict User Membership to the Federation

You can prevent users in your Federated Authentication instance from creating
new organizations or using their credentials to access organizations outside
of the federation. Configure this setting for full control of your federated
users and to help ensure that federated users only have access to desired
Atlas organizations.

## Important

This setting applies to the _entire_ federation, including all Identity
Providers and Organizations within the federation.

### Considerations

Once you enable this setting:

  * No users in your Federated Authentication instance can gain access to organizations outside of your federation.

    * Similarly, no federated users can accept or receive invitations to join organizations outside of your federation.

  * Users in your federation with the `Organization Owner` role can still create new organizations. These new organizations are automatically connected to your federation.

  * Users in your federation without the `Organization Owner` role cannot create any new organizations.

  * Users in your federation retain access to any organizations they had access to prior to the membership restriction.

### Procedure

From the Federation Management Console:

1

#### Click Advanced Settings in the left navigation pane.

2

#### Toggle Restrict Membership to On.

3

#### View User Conflicts

If your federation contains users who belong to organizations outside of your
federation, Atlas displays a warning banner. To review the conflicting users,
click View User Conflicts.

Atlas displays a modal with a list of users that conflict with the federation
restriction. Consider contacting these users to make them aware of the
restriction.

← Configure Federated Authentication from OktaManage Your Multi-Factor
Authentication Options →

