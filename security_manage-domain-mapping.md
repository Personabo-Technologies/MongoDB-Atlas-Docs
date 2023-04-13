Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Domain Mapping for Federated Authentication

Share Feedback

On this page

  * Prerequisites
  * Federation Management Access
  * Map a Domain to Your Identity Provider
  * Associate Your Domain with Your Identity Provider
  * Delete a Domain Mapping

You can map domains to your IdP to streamline the login experience for users
from specified domains by authenticating them through an IdP. Domain mapping
ensures that all users with a particular domain in their email address have
the same login experience.

## Important

You can map a single domain to multiple identity providers. If you do, users
who log in using the MongoDB Cloud console are automatically redirected to the
first matching IdP mapped to the domain.

To log in using an alternative identity provider, users must either:

  * Initiate the MongoDB Cloud login through the desired IdP, or

  * Log in using the Login URL associated with the desired IdP.

To map a domain to your IdP, you must verify that you own the domain. You can
either:

  * Upload an HTML file containing a verification key to a host in your domain or

  * Create a DNS TXT record that contains a verification key.

## Prerequisites

To complete this tutorial, you must have already linked an IdP to Atlas. To
learn how to link an IdP to Atlas, see Manage Identity Providers.

## Federation Management Access

You can manage federated authentication from the Federation Management
Console. You can access the console as long as you are an `Organization Owner`
in one or more organizations that are delegating federation settings to the
instance.

## Map a Domain to Your Identity Provider

1

### Open the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

2

### Enter domain mapping information.

  1. Click Add a Domain.

  2. On the Domains screen, click Add Domain.

  3. Enter the following information for your domain mapping:

Field

|

Description  
  
|  
  
Display Name

|

Name to easily identify the domain.  
  
Domain Name

|

Domain name to map.  
  
  4. Click Next.

3

### Choose how to verify your domain.

## Note

You can choose the verification method once. It cannot be modified. To select
a different verification method, delete and recreate the domain mapping.

Select the appropriate tab based on whether you are verifying your domain by
uploading an HTML file or creating a DNS TXT record:

Upload HTML File

Create DNS Record

Upload an HTML file containing a verification key to verify that you own your
domain.

  1. Click HTML File Upload.

  2. Click Next.

  3. Download the `mongodb-site-verification.html` file that Atlas provides.

  4. Upload the HTML file to a web site on your domain. You must be able to access the file at `<https://host.domain>/mongodb-site-verification.html`.

  5. Click Finish.

4

### Verify your domain.

The Domains screen displays both unverified and verified domains you've mapped
to your IdP. To verify your domain, click the target domain's Verify button.
Atlas shows whether the verification succeeded in a banner at the top of the
screen.

## Associate Your Domain with Your Identity Provider

After successfully verifying your domain, associate the domain with your IdP:

1

### Click Identity Providers in the left navigation.

2

### For the IdP you want to associate with your domain, click __ Edit next to
Associated Domains.

3

### Select the domain you want to associate with the IdP.

4

### Click Confirm.

### Test Your Domain Mapping

## Important

Before you begin testing, copy and save the Bypass SAML Mode URL for your IdP.
Use this URL to bypass federated authentication in the event that you are
locked out of your Atlas organization.

While testing, keep your session logged in to the Federation Management
Console to further ensure against lockouts.

To learn more about Bypass SAML Mode, see Bypass SAML Mode.

To test the integration between your domain and your IdP:

1

#### In a private browser window, navigate to the Atlas log in page.

2

#### Enter a username (usually an email address) with your verified domain.

## Example

If your verified domain is `mongodb.com`, enter `alice@mongodb.com`.

3

#### Click Next.

If you mapped your domain correctly, you're redirected to your IdP to
authenticate. If authenticating with your IdP succeeds, you're redirected back
to Atlas.

## Note

You can bypass the Atlas log in page by navigating directly to your IdP's
Login URL. The Login URL takes you directly to your IdP to authenticate.

## Delete a Domain Mapping

### Open the Federation Management Console

1

#### Navigate to the Settings page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click the Organization Settings icon next to the Organizations menu.

2

#### Navigate to the Federation Management App.

In the Setup Federated Login or Manage Federation Settings section, click
Visit Federation Management App.

### Delete the Domain

1

#### Open the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

2

#### Delete the domain.

## Important

You cannot delete a domain mapping if it is associated with an IdP. To
disassociate a domain from an IdP:

  1. From the management console, click Identity Providers
    in the left navigation.
  2. For the IdP you want to disassociate from your domain, click
     __ Edit next to Associated Domains.
  3. Deselect the domain desired domain.

  4. Click Confirm.

To delete a domain from the Federation Management instance:

  1. Click Add a Domain.

  2. Open the Actions menu for the domain you want to delete.

  3. Click Delete.

  4. Click Confirm.

← Manage Identity ProvidersManage Organization Mapping for Federated
Authentication →

