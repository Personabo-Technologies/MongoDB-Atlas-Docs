Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Your Multi-Factor Authentication Options

Share Feedback

On this page

  * Considerations
  * Prerequisites
  * Enable Multi-Factor Authentication
  * Remove an Authentication Method

Authentication verifies the identity of a user. The process uses either
something you _have_ or something you _know_. You _know_ your password. You
_have_ an app that gives you a one-time token. Multi-factor authentication
(MFA) uses both.

## Considerations

## Important

To use MFA, an `Organization Owner` must enable it for their organization. All
members of that organization must enable MFA for their accounts. Those members
who haven't enabled MFA can't access the organization.

When enabling MFA, Atlas requests two forms of identification: your password
and one of the following factors:

  * Okta Verify Mobile App

  * WebAuthn

  * Google Authenticator

  * Email

  * SMS

### Set Up Backup Multi-Factor Authentication Methods

## Warning

Enable a minimum of two methods so that you can still access your account if
you lose access to one method.

While you can set up one, some, or all of the available methods, we strongly
recommend that you set up at least two methods. When Atlas requires MFA, it
offers you the choice of which method to use. If you have less than two
methods set up, Atlas prompts you to set up MFA and a backup method at login.

## Prerequisites

### Disable Legacy Two-Factor Authentication

If you use legacy two-factor authentication, disable it before setting up MFA.

To disable legacy 2FA, complete the following procedure:

  1. Click on your name in the upper right corner of the Atlas console. A dropdown menu displays.

  2. Click User Preferences.

  3. Click Legacy 2FA on the left-hand menu.

  4. Click __ Edit.

### Install MFA Mechanism

Install and configure the second authentication factor.

Okta Verify Mobile App

Security Key / Biometric

Authenticator App

Email

SMS

Download the Okta Verify app to your iOS or Android device.

## Enable Multi-Factor Authentication

1

### Navigate to the Account Security page.

  1. Click on your name in the upper right corner of the Atlas console. A dropdown menu displays.

  2. Click Manage your MongoDB Account.

  3. Click Security in the left-side navigation.

2

### Set up an authentication method.

  1. Choose your preferred authentication method.

  2. Click Set up to the right of your chosen method.

  3. Follow the procedure for your chosen method:

Okta Verify Mobile App

Security Key / Biometric

Authenticator App

Email

SMS

Complete these steps using the Okta Verify mobile app.

  1. Open the Okta Verify app on your mobile device.

  2. Tap the + icon to add an account. The app places this icon in the app's menu bar at the top of the screen.

  3. Scan the bar code displayed in Atlas.

  4. Click Done.

3

### Choose another authentication method.

After you set up your first authentication method, repeat the steps to set up
another method.

## Remove an Authentication Method

To remove a method from your account:

  1. Choose a method to remove.

  2. Click __ Delete to the right of that method.

To remove a method, Atlas asks you to authenticate again using MFA.

← Advanced Options for Federated AuthenticationLegacy Two-Factor
Authentication →

