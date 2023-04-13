Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Federated Authentication from Google Workspace

Share Feedback

On this page

  * Limitations
  * Prerequisites
  * Procedures
  * Configure Google Workspace as an Identity Provider
  * (Optional) Map an Organization
  * (Optional) Configure Advanced Federated Authentication Options
  * Sign in to Atlas Using Your Login URL

This guide shows you how to configure federated authentication using Google
Workspace as your IdP.

After integrating Google Workspace and Atlas, you can use your company's
credentials to log in to Atlas and other MongoDB cloud services.

## Limitations

Atlas doesn't support single sign-on integration for database users. If you
implement Google Workspace as your IdP, you cannot use the Log In with Google
social login option.

## Prerequisites

To use Google Workspace as an IdP for Atlas, you must have:

  * A Google Workspace subscription. To obtain a subscription, visit the Google Workspace portal.

  * A Google Workspace user with administrative privileges. To grant a user administrative privileges, see Make a user an admin. Alternatively, you may use the default administrative user created upon activation of your Google Workspace account.

## Procedures

### Configure Google Workspace as an Identity Provider

Use the Google Workspace admin console to configure Google Workspace as a SAML
IdP.

1

#### Add a new application to your Google Workspace account.

  1. In your Google Workspace administrator account, open the Apps dropdown menu and click Web and mobile apps.

  2. Open the Add App dropdown menu and click Add custom SAML app.

  3. Enter a name to identify the app , such as "MongoDB Cloud," in the App name field.

  4. Select an App icon if desired.

  5. Click the Continue button.

2

#### Retrieve SSO credentials from Google Workspace.

  1. Navigate to the Option 2 section.

  2. Copy the SSO URL and Entity ID, and download the Certificate provided. These will be used by the FMC in a subsequent step. Leave this page open.

3

#### Navigate to the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

4

#### Provide Google Workspace Credentials to Atlas.

  1. Click Identity Providers in the left-hand pane. If you have previously configured an IdP, click Add Identity Provider in the upper-right corner of the page, then click Setup Identity Provider. If you have not previously configured an IdP, click Setup Identity Provider.

  2. On the Create Identity Provider screen, enter the following information:

Field

|

Value  
  
|  
  
Configuration Name

|

A descriptive name that identifies the configuration.  
  
Issuer URI

|

Provide the Entity ID you received from Google Workspace in the previous step.  
  
Single Sign-On URL

|

Provide the SSO URL you received from Google Workspace in the previous step.  
  
Identity Provider Signature Certificate

|

Provide the `.cer` file you received from Google Workspace in the previous
step.

You can either:

    * Upload the certificate from your computer

    * Paste the contents of the certificate into a text box  
  
Request Binding

|

`HTTP POST`  
  
Response Signature Algorithm

|

`SHA-256`  
  

  1. Click the Next button.

5

#### Get Atlas Metadata for Google Workspace.

  1. In the FMC, copy the Assertion Consumer Service URL and Audience URI.

  2. Click the Finish button.

  3. Copy the Login URL on the IdP tile that Google Workspace creates for your application.

6

#### Provide Atlas Metadata to Google Workspace.

  1. Return to the Google Workspace configuration page and click the Continue button.

  2. Fill in the data fields with the following values:

Field

|

Value  
  
|  
  
ACS URL

|

The Assertion Consumer Service URL provided by Atlas.  
  
Entity ID

|

The Audience URI provided by Atlas.  
  
Start URL

|

The Login URL provided by Atlas.  
  
Signed Response

|

Check this box.  
  
Name ID Format

|

`UNSPECIFIED`  
  
Name ID

|

`Basic Information > Primary Email`  
  
  3. Click the Continue button.

7

#### Configure Google Workspace Attributes.

  1. In Google Workspace, add each of the following value pairs as distinct mappings by clicking the Add Mapping button for each pair. App attribute values are case-sensitive.

Google Directory attributes

|

App attributes  
  
|  
  
Basic Information > First name

|

`firstName`  
  
Basic Information > Last name

|

`lastName`  
  
  2. If you are configuring role mapping, proceed to the next step. Otherwise, click the Finish button and proceed to **Enable User Access via Google Workspace**.

8

#### (Optional) Configure role mapping.

  1. To configure role mapping in Google Workspace, create a single group attribute in the Group membership (optional) section as follows:

|  
  
|  
  
Google groups

|

Search for and select all Google groups which you intend to map to Atlas
roles, ensuring that they are all included in a single row. For more
information on this attribute, consult About group membership mapping.  
  
App attributes

|

`memberOf`  
  
  2. Click the Finish button.

9

#### Enable User Access via Google Workspace.

  1. Click the arrow in the top-right corner of the User Access panel to expand it.

  2. Enable user access. You can either:

    * Click ON for everyone in the Service status pane to enable federated authentication for all users in your Google Workspace.

    * Select specific Groups or Organizational Units from the collapsible menus on the left for which you wish to enable federated authentication. The Google Workspace help pages provide more information on managing Groups and Organizational Units.

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
Console to associate the domain with Google Workspace:

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
domain and Google Workspace:

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

All users that you assign to the Google Workspace application can log in to
Atlas using their Google Workspace credentials on the Login URL. Users have
access to the organizations you mapped to your IdP.

## Important

You can map a single domain to multiple identity providers. If you do, users
who log in using the MongoDB Cloud console are automatically redirected to the
first matching IdP mapped to the domain.

To log in using an alternative identity provider, users must either:

  * Initiate the MongoDB Cloud login through the desired IdP, or

  * Log in using the Login URL associated with the desired IdP.

If you select a default organization role, new users who log in to Atlas using
the Login URL have the role you specify

← Configure Federated Authentication from Azure ADConfigure Federated
Authentication from Okta →

