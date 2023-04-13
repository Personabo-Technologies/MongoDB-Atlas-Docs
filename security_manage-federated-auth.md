Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Identity Providers

Share Feedback

On this page

  * Federation Management Access
  * Procedure
  * Configure An External Identity Provider Application
  * Apply Your Identity Provider to Atlas
  * Configure Your Identity Provider with Atlas Metadata
  * Next Steps

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

The following procedure walks you through linking an IdP to Atlas.

## Federation Management Access

You can manage federated authentication from the Federation Management
Console. You can access the console as long as you are an `Organization Owner`
in one or more organizations that are delegating federation settings to the
instance.

## Procedure

## Important

### Two-Stage Configuration

Depending on your Identity Provider, some circular logic may apply when
linking it to a Service Provider like Atlas. To link your IdP to Atlas:

  * Your IdP needs values from Atlas and

  * Atlas needs values from your IdP.

To simplify setup, Atlas prompts you to enter placeholder values for the IdP
and Atlas configurations. You will replace these values later in the
procedure.

### Configure An External Identity Provider Application

To configure Federated Authentication, you must have an external SAML IdP
application. In the SAML IdP, you must:

  1. Create a new application for Atlas.

  2. Configure initial SAML values for the new application:

    1. Set placeholder values for the following fields:

      * SP Entity ID or Issuer

      * Audience URI

      * Assertion Consumer Service (ACS) URL

    2. Set valid values for the following fields:

Field

|

Value  
  
|  
  
Signature Algorithm

|

The signature algorithm is the algorithm used to encrypt the IdP signature.
Atlas supports the following signature algorithm values:

      * `SHA-1`

      * `SHA-256`  
  
Name ID

|

A valid email address.

## Important

Name ID is both your email address and username.  
  
Name ID Format

|

`urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`  
  
    3. Create attributes with the following Attribute Names for the following SAML Attribute Values:

SAML Attribute Name

|

SAML Attribute Value  
  
|  
  
`firstName`

|

First Name  
  
`lastName`

|

Last Name  
  
`memberOf`

|

User Groups  
  
## Note

The names of these attributes are case sensitive. Type these attribute names
as shown in camelCase.

    4. Save these values.

Once you have completed the initial setup for your IdP application, you link
the IdP to Atlas to federate your users' logins.

### Apply Your Identity Provider to Atlas

## Note

### Prerequisite

This procedure assumes you already have an external IdP. To learn how to
configure an IdP, see Configure An External Identity Provider Application.

You can configure Federated Authentication in Atlas from the Federation
Management Console. Use this console to:

  * Configure Identity Providers to authenticate users belonging to specified organizations.

  * Connect Atlas Organizations to your IdP.

  * Verify and associate Domains with your IdP to force users to authenticate using that IdP.

#### Open the Management Console

1

##### Navigate to the Settings page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click the Organization Settings icon next to the Organizations menu.

2

##### Navigate to the Federation Management App.

In the Setup Federated Login or Manage Federation Settings section, click
Visit Federation Management App.

#### From the Management Console:

  1. Click Add Identity Providers

  2. If you do not have any Identity Providers configured yet, click Setup Identity Provider. Otherwise, On the Identity Providers screen, click Add Identity Provider.

  3. Enter or select the following SAML Protocol Settings. All fields are required:

Field

|

Description  
  
|  
  
Configuration Name

|

Name of this IdP configuration.  
  
IdP Issuer URI

|

Identifier for the issuer of the SAML Assertion.

## Note

Specify a placeholder value for this field. Obtain the real value for this
field from your IdP once you have supplied it with the Atlas metadata.  
  
IdP Single Sign-On URL

|

URL of the receiver of the SAML AuthNRequest.

## Note

Specify a placeholder value for this field. Obtain the real value for this
field from your IdP once you have supplied it with the Atlas metadata.  
  
IdP Signature Certificate

|

PEM-encoded public key certificate of the IdP. You can obtain this value from
your IdP.

You can either:

    * Upload the certificate from your computer, or

    * Paste the contents of the certificate into a text box.  
  
Request Binding

|

SAML Authentication Request Protocol binding used to send the AuthNRequest.
Can be either:

    * `HTTP POST`

    * `HTTP REDIRECT`  
  
Response Signature Algorithm

|

Response algorithm used to sign the SAML AuthNRequest. Can be either:

    * `SHA-256`

    * `SHA-1`  
  
  4. Click Next.

### Configure Your Identity Provider with Atlas Metadata

Having set up your IdP in Atlas, you can provide the required Atlas metadata
to your IdP.

  1. On the Identity Provider screen in Atlas, click Download metadata to download the metadata required by your IdP. Atlas provides the data as an `.xml` file.

click to enlarge

## Note

Atlas provides the Assertion Consumer Service URL and Audience URI if you wish
to manually copy and save these values. These values are included in the
metadata download.

## Note

The SAML trust model requires certificate exchange over trusted channels
during setup and doesn't require CA-signed certificates. During federated
authentication, all traffic between MongoDB Atlas and the browser runs over
TLS using a CA-signed certificate. Therefore, `metadata.xml` provides only a
self-signed certificate for request signing and signature validation.

  2. Upload the metadata to your IdP.

You now have the necessary information to replace the placeholder IdP Issuer
URI and IdP Single Sign-On URL values set when you set up the initial IdP
mapping in Atlas.

  3. In Atlas, modify the placeholder values set for IdP Issuer URI and IdP Single Sign-On URL for the linked IdP with the proper values from your IdP.

  4. Optionally, add a RelayState URL to your IdP to send users to a URL you choose and avoid unnecessary redirects after login. You can use:

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
      
  
  5. Return to Atlas and click Finish.

## Important

Once you link your IdP to Atlas, it shows as Inactive in the Federation
Management Console until you map at least one domain to the IdP.

## Next Steps

After you successfully linked your IdP to Atlas, you must map one or more
domains to your Identity Provider. Atlas authenticates users from these
domains through your IdP.

← Configure Federated AuthenticationManage Domain Mapping for Federated
Authentication →

