Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Federated Authentication from Okta

Share Feedback

On this page

  * Limitations
  * Prerequisites
  * Procedures
  * Configure Okta as an Identity Provider
  * (Optional) Map an Organization
  * (Optional) Configure Advanced Federated Authentication Options
  * Sign in to Atlas Using Your Login URL

This guide shows you how to configure federated authentication using Okta as
your IdP.

After integrating Okta and Atlas, you can use your company's credentials to
log in to Atlas and other MongoDB cloud services.

## Note

If you are using Okta's built-in MongoDB Cloud app, you can use Okta's
documentation.

If you are creating your own SAML app, use the procedures described here.

## Limitations

Atlas doesn't support single sign-on integration for database users. If you
implement Okta as your IdP, you cannot use the Log In with Google social login
option.

## Prerequisites

To use Okta as an IdP for Atlas, you must have:

  * An Okta account.

  * A custom, routable domain name.

## Procedures

Throughout the following procedure, it is helpful to have one browser tab open
to your Atlas Federation Management Console and one tab open to your Okta
account.

### Configure Okta as an Identity Provider

1

#### Add a new application to your Okta account

  1. In the Okta top navigation, click the Applications tab.

  2. Click the Add Application button.

  3. Click the Create New App button.

  4. Select Web for the Platform field.

  5. Select SAML 2.0 for the Sign on method field.

  6. Click the Create button.

2

#### Create Okta SAML integration

  1. Fill in the App name text field with your desired application name.

  2. Optionally, add a logo image and set app visibility.

  3. Click the Next button.

3

#### Download Okta certificate

  1. Click the Download Okta Certificate button.

  2. Rename the downloaded file to have a `.cer` extension instead of `.cert`.

4

#### Navigate to the Federation Management Console

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

5

#### Create a new Identity Provider

  1. In the FMC dashboard, click the Manage Identity Providers button.

  2. Click the Setup Identity Provider button.

6

#### Enter SAML settings

  1. In the FMC dashboard, fill in the data fields with the following values:

Field

|

Value  
  
|  
  
Configuration Name

|

A descriptive name of your choosing.  
  
Issuer URI and Single Sign-On URL

|

Click the Fill With Placeholder Values button to the right of the text fields.
You will get the real values from Okta in a later step.  
  
Identity Provider Signature Certificate

|

Provide the `.cer` file you received from Okta earlier.

You can either:

    * Upload the certificate from your computer, or

    * Paste the contents of the certificate into a text box.  
  
Request Binding

|

HTTP POST  
  
Response Signature Algorithm

|

SHA-256  
  
  2. Click the Next button.

7

#### Create SAML Integration

  1. In this step, copy values from the Atlas FMC to the Okta Create SAML Integration page.

Okta Data Field

|

Value  
  
|  
  
Single sign on URL

|

Use the Assertion Consumer Service URL from the Atlas FMC.

Checkboxes:

    * Check Use this for Recipient URL and Destination URL.

    * Clear Allow this app to request other SSO URLs.  
  
Audience URI (SP Entity ID)

|

Use the Audience URI from the Atlas FMC.  
  
Default RelayState

|

Optionally, add a RelayState URL to your IdP to send users to a URL you choose
and avoid unnecessary redirects after login. You can use:

|

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
      
  
Name ID format

|

Unspecified  
  
Application username

|

Email  
  
Update application username on

|

Create and update  
  
  2. Click the Click Show Advanced Settings link in the Okta configuration page and ensure that the following values are set:

Okta Data Field

|

Value  
  
|  
  
Response

|

Signed  
  
Assertion Signature

|

Signed  
  
Signature Algorithm

|

RSA-SHA256  
  
Digest Algorithm

|

SHA256  
  
Assertion Encryption

|

Unencrypted  
  
  3. Leave the remaining Advanced Settings fields in their default state.

  4. Scroll down to the Attribute Statements (optional) section and create four attributes with the following values:

Name

|

Name Format

|

Value  
  
||  
  
firstName

|

Unspecified

|

user.firstName  
  
lastName

|

Unspecified

|

user.lastName  
  
## Important

The values in the **Name** column are case-sensitive. Enter them exactly as
shown.

## Note

These values may be different if Okta is connected to an Active Directory. For
the appropriate values, use the Active Directory fields that contain a user's
first name, last name, and full email address.

  5. (Optional) If you plan to use role mapping, scroll down to the Group Attribute Statements (optional) section and create an attribute with the following values:

Name

|

Name Format

|

Filter

|

Value  
  
|||  
  
memberOf

|

Unspecified

|

Matches regex

|

`.*`  
  
This filter matches all group names associated with the user. To filter the
group names sent to Atlas further, adjust the Filter and Value fields.

  6. Click the Next button in the Okta configuration.

  7. Select the radio button marked I'm an Okta customer adding an internal app.

  8. Click the Finish button.

8

#### Copy information back to the Atlas FMC

  1. On the Okta application page, click View Setup Instructions in the middle of the page.

## Note

The Okta setup instructions appear in a new browser tab.

  2. In the Atlas FMC, click the Finish button to return to the Identity Providers page. Click the Modify button for your newly created IdP.

  3. Fill in the following text fields:

FMC Data Field

|

Value  
  
|  
  
Issuer URI

|

Use the Identity Provider Issuer value from the Okta Setup Instructions page.  
  
Single Sign-on URL

|

Use the Identity Provider Single Sign-On URL value from the Okta Setup
Instructions page.  
  
  4. Close the Okta setup instructions browser tab.

  5. Click the Next button on the Atlas FMC page.

  6. Click the Finish button the FMC Edit Identity Provider page.

9

#### Assign users to your Okta application

  1. On the Okta application page, click the Assignments tab.

  2. Ensure that all your Atlas organization users who will use the Okta service are enrolled.

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
Console to associate the domain with Okta:

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
domain and Okta:

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

All users you assigned to the Okta application can log in to Atlas using their
Okta credentials on the Login URL. Users have access to the organizations you
mapped to your IdP.

## Important

You can map a single domain to multiple identity providers. If you do, users
who log in using the MongoDB Cloud console are automatically redirected to the
first matching IdP mapped to the domain.

To log in using an alternative identity provider, users must either:

  * Initiate the MongoDB Cloud login through the desired IdP, or

  * Log in using the Login URL associated with the desired IdP.

If you selected a default organization role, new users who log in to Atlas
using the Login URL have the role you specified.

← Configure Federated Authentication from Google WorkspaceAdvanced Options for
Federated Authentication →

