Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Federated Authentication from Azure AD

Share Feedback

On this page

  * Limitations
  * Prerequisites
  * Procedures
  * Add Domain users
  * Configure Azure AD as an Identity Provider
  * Add Azure AD as an Identity Provider in Atlas
  * (Optional) Map an Organization
  * (Optional) Configure Advanced Federated Authentication Options
  * Sign in to Atlas Using Your Login URL

This guide shows you how to configure federated authentication using Azure AD
as your IdP.

After integrating Azure AD and Atlas, you can use your company's credentials
to log in to Atlas and other MongoDB cloud services.

## Limitations

Atlas doesn't support single sign-on integration for database users. To
configure Atlas to authenticate and authorize database users from Azure AD
using LDAP, see Configure User Authentication and Authorization with Azure AD
Domain Services.

## Prerequisites

To use Azure AD as an IdP for Atlas, you must have:

  * An Azure subscription. To obtain a subscription, visit the Microsoft Azure portal.

  * An Azure AD tenant associated with your subscription. For information about setting up an Azure AD tenant, see the Azure AD Documentation.

  * `Global Administrator` privileges in your Azure AD tenant.

  * A custom, routable domain name.

## Procedures

### Add Domain users

If you haven't already, use the Azure console to add your custom domain name
to Azure AD and create users:

1

#### Add your custom domain to Azure AD.

Add your custom domain name to Azure AD to create users that belong to your
domain. After you add your domain, you must also add the Azure AD DNS
information in a `TXT` record with your DNS provider and verify the
configuration.

To add your custom domain to Azure AD, see the Azure documentation.

2

#### Create Azure AD Users.

If they don't exist already, create users in Azure AD that you want to grant
database access to. Users must belong to the custom domain you added to Azure
AD.

To create Azure AD users, see the Azure documentation.

### Configure Azure AD as an Identity Provider

Use the Azure console to configure Azure AD as a SAML IdP. You can either add
the MongoDB Cloud app from the Gallery or configure an application manually.

Use the MongoDB Cloud Gallery App

Configure an App Manually

1

#### Add the MongoDB Cloud app from the gallery.

To add the MongoDB Cloud app to your Azure AD tenant, see the Azure
documentation.

## Tip

### See also:

MongoDB Cloud on the Azure Marketplace

2

#### Assign users to the application.

Assign users to the application. These users will have access to Atlas and
other MongoDB cloud services when you complete the tutorial.

To assign Azure AD users to an application, see the Azure documentation.

3

#### Navigate to the SAML configuration page to begin configuring single sign-
on.

To navigate to the SAML configuration page, see the Azure documentation.

4

#### Set temporary values for the Identifier and Reply URL.

To generate a valid SAML signing certificate, you must assign temporary values
to the Identifier and Reply URL for your Azure AD enterprise application. If
you download the certificate before setting these values, the downloaded
certificate won't be unique and you must download the certificate again after
setting these values.

To set the temporary values:

  1. Click Edit in Section 1.

  2. Remove any existing default values and set the following temporary values:

Setting

|

Temporary Value  
  
|  
  
Identifier (Entity ID)

|

`https://www.okta.com/saml2/service-provider/MongoDBCloud`  
  
Reply URL (Assertion Consumer Service URL).

|

`https://auth.mongodb.com/sso/saml2/`  
  
  3. Click Save.

  4. Refresh the browser page to ensure that the certificate is regenerated.

The certificate's thumbprint and expiration date change from the values they
held after the temporary Identifier and Reply URL are updated for the first
time.

5

#### Download the SAML signing certificate encoded in `Base64`.

In the SAML Signing Certificate section, click Download next to Certificate
(Base64).

You upload this signing certificate to the MongoDB Federation Management
Console later in the tutorial.

6

#### Optional: Add group claims to the SAML token.

Skip this step if you won't use role mapping.

To use role mapping, add the following group claim to the SAML token Azure AD
sends to Atlas:

  1. Click Add a group claim. Azure displays the Group Claims panel.

  2. In Which groups associated with the user should be returned in the claim?, click Security groups.

What groups you select depend on the type of groups you configured in your
Azure environment. You may need to select a different type of group to send
the appropriate group information.

  3. From the Source attribute dropdown menu, click Group Id.

If you select Group Id, Azure sends the security group's Object ID and not the
human-readable group name. Depending on your Azure environment, you may have
the option to select a different source attribute which sends the group name
instead.

When creating role mappings in Atlas, match the Azure group data sent in the
SAML response to the configured Atlas role mapping name exactly.

  4. Click Customize the name of the group claim in the Advanced options section.

  5. Set Name to **memberOf**.

  6. Leave Namespace blank.

  7. Clear Emit groups as role claims.

  8. Click Save.

7

#### Copy the values of the Login URL and Azure AD Identifier fields.

Paste these values into a text editor or another easily accessible location.

You enter these values in the MongoDB Federation Management Console later in
the tutorial.

### Add Azure AD as an Identity Provider in Atlas

Use the Federation Management Console and the Azure console to add Azure AD as
an IdP:

1

#### Open the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

2

#### Add Azure AD to Atlas as an Identity Provider.

  1. Click Add Identity Providers

  2. If you do not have any Identity Providers configured yet, click Setup Identity Provider. Otherwise, On the Identity Providers screen, click Add Identity Provider.

  3. Enter or select the following SAML Protocol Settings. All fields are required:

Field

|

Description  
  
|  
  
Configuration Name

|

Enter a descriptive name, such as `Azure AD`.  
  
IdP Issuer URI

|

Paste the Azure AD Identifier you copied from Azure earlier in the tutorial.  
  
IdP Single Sign-On URL

|

Paste the Login URL you copied from Azure earlier in the tutorial.  
  
IdP Signature Certificate

|

Provide the `Base64`-encoded SAML signing certificate you downloaded from
Azure earlier in the tutorial.

You can either:

    * Upload the certificate from your computer, or

    * Paste the contents of the certificate into a text box.  
  
Request Binding

|

Select HTTP POST.  
  
Response Signature Algorithm

|

Select SHA-256.  
  
  4. Click Next.

3

#### Download the metadata file with details that recognize MongoDB as a
Service Provider.

  1. Click Download metadata. You upload this file to Azure AD in the next step.

  2. Click Finish.

4

#### Upload the metadata file to Azure to finish configuring Azure AD as an
IdP.

To upload the file, see the screenshot in step 3 of Enable single sign-on for
an app in the Azure documentation. Click Upload metadata file on the SSO
configuration page, as shown in the screenshot in the linked Azure
documentation.

Optionally, add a RelayState URL to your IdP to send users to a URL you choose
and avoid unnecessary redirects after login. You can use:

Destination

|

RelayState URL  
  
|  
  
MongoDB Atlas

|

The Login URL that was generated for your identity provider configuration in
the Atlas Federation Management App.  
  
MongoDB Support Portal

|

    
    
    | https://auth.mongodb.com/app/salesforce/exk1rw00vux0h1iFz297/sso/saml  
      
  
MongoDB University

|

    
    
    | https://university.mongodb.com  
      
  
MongoDB Community Forums

|

    
    
    | https://auth.mongodb.com/home/mongodbexternal_communityforums_3/0oa3bqf5mlIQvkbmF297/aln3bqgadajdHoymn297  
      
  
MongoDB Feedback Engine

|

    
    
    | https://auth.mongodb.com/home/mongodbexternal_uservoice_1/0oa27cs0zouYPwgj0297/aln27cvudlhBT7grX297  
      
  
MongoDB JIRA

|

    
    
    | https://auth.mongodb.com/app/mongodbexternal_mongodbjira_1/exk1s832qkFO3Rqox297/sso/saml  
      
  
#### Map your Domain

Mapping your domain to the IdP lets Atlas know that users from your domain
should be directed to the Login URL for your identity provider configuration.

When users visit the Atlas login page, they enter their email address. If the
email domain is associated with an IdP, they are sent to the Login URL for
that IdP.

## Important

You can map a single domain to multiple identity providers. If you do, users
who log in using the MongoDB Cloud console are automatically redirected to the
first matching IdP mapped to the domain.

To log in using an alternative identity provider, users must either:

  * Initiate the MongoDB Cloud login through the desired IdP, or

  * Log in using the Login URL associated with the desired IdP.

Use the Federation Management Console to map your domain to the IdP:

1

##### Open the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

2

##### Enter domain mapping information.

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

##### Choose how to verify your domain.

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

##### Verify your domain.

The Domains screen displays both unverified and verified domains you've mapped
to your IdP. To verify your domain, click the target domain's Verify button.
Atlas shows whether the verification succeeded in a banner at the top of the
screen.

#### Associate Your Domain with Your Identity Provider

After successfully verifying your domain, use the Federation Management
Console to associate the domain with Azure AD:

1

##### Click Identity Providers in the left navigation.

2

##### For the IdP you want to associate with your domain, click __ Edit next
to Associated Domains.

3

##### Select the domain you want to associate with the IdP.

4

##### Click Confirm.

#### Test Your Domain Mapping

## Important

Before you begin testing, copy and save the Bypass SAML Mode URL for your IdP.
Use this URL to bypass federated authentication in the event that you are
locked out of your Atlas organization.

While testing, keep your session logged in to the Federation Management
Console to further ensure against lockouts.

To learn more about Bypass SAML Mode, see Bypass SAML Mode.

Use the Federation Management Console to test the integration between your
domain and Azure AD:

1

##### In a private browser window, navigate to the Atlas log in page.

2

##### Enter a username (usually an email address) with your verified domain.

## Example

If your verified domain is `mongodb.com`, enter `alice@mongodb.com`.

3

##### Click Next.

If you mapped your domain correctly, you're redirected to your IdP to
authenticate. If authenticating with your IdP succeeds, you're redirected back
to Atlas.

## Note

You can bypass the Atlas log in page by navigating directly to your IdP's
Login URL. The Login URL takes you directly to your IdP to authenticate.

### (Optional) Map an Organization

Use the Federation Management Console to assign your domain's users access to
specific Atlas organizations:

1

#### Open the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

2

#### Connect an organization to the Federation Application.

  1. Click View Organizations.

Atlas displays all organizations where you are an `Organization Owner`.

Organizations which are not already connected to the Federation Application
have Connect button in the Actions column.

  2. Click the desired organization's Connect button.

3

#### Apply an Identity Provider to the organization.

From the Organizations screen in the management console:

  1. Click the Name of the organization you want to map to an IdP.

  2. On the Identity Provider screen, click Apply Identity Provider.

Atlas directs you to the Identity Providers screen which shows all IdPs you
have linked to Atlas.

  3. For the IdP you want to apply to the organization, click Add Organizations.

  4. In the Apply Identity Provider to Organizations modal, select the organizations to which this IdP applies.

  5. Click Confirm.

4

#### Connect an organization to the Federation Application.

  1. Click Organizations in the left navigation.

  2. In the list of Organizations, ensure that your desired organization(s) now have the expected Identity Provider.

### (Optional) Configure Advanced Federated Authentication Options

You can configure the following advanced options for federated authentication
for greater control over your federated users and authentication flow:

  * Bypass SAML Mode

## Note

The following advanced options for federated authentication require you to map
an organization.

  * Assign a Default User Role for an Organization

  * Restrict Access to an Organization by Domain

  * Restrict User Membership to the Federation

## Sign in to Atlas Using Your Login URL

All users you assigned to the Azure application can log in to Atlas using
their Azure AD credentials on the Login URL. Users have access to the
organizations you mapped to your IdP.

## Important

You can map a single domain to multiple identity providers. If you do, users
who log in using the MongoDB Cloud console are automatically redirected to the
first matching IdP mapped to the domain.

To log in using an alternative identity provider, users must either:

  * Initiate the MongoDB Cloud login through the desired IdP, or

  * Log in using the Login URL associated with the desired IdP.

If you selected a default organization role, new users who log in to Atlas
using the Login URL have the role you specified.

← Manage Mapping Atlas Roles to IdP GroupsConfigure Federated Authentication
from Google Workspace →

