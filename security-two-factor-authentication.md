Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Legacy Two-Factor Authentication

Share Feedback

On this page

  * Configure Two-Factor Authentication
  * Configure Backup Two Factor Authentication Phone Number
  * Generate New Recovery Codes
  * Reset Legacy Two Factor Authentication

## Important

Legacy 2FA is deprecated. If you currently have legacy 2FA enabled you can
continue to use it, but it is recommended that you switch to multi-factor
authentication. To use MFA, disable legacy two-factor authentication and
enable multi-factor authentication instead.

If an `Organization Owner` enables MFA, all organization members must also
enable MFA before accessing that organization.

Two-factor authentication provides a second layer of security for your Atlas
account. If you enable 2FA for your account and after you enter your username
and password, you are prompted for a six-digit time-sensitive verification
code. This code is sent to a separate device, such as a mobile phone or
security token, that you can read and enter into Atlas and complete your
login.

## Note

  * An Atlas `Organization Owner` can require that all Atlas users within their organization enable 2FA for their Atlas accounts. For more information, see Require Multi-Factor Authentication.

  * If you login using your Google account:

Google manages your 2FA. You can't use Atlas multi-factor authentication and
won't be prompted for an Atlas 2FA verification when you log into Atlas.
Google should verify your identity using Google 2-Step Verification.

To learn more about organization settings, see Change Organization Settings.

Atlas provides the following sources for 2FA verification codes:

Text or Voice

2FA App

2FA device

 **Text Messages** (SMS)

When Atlas prompts you for a verification code, Atlas sends the 6-digit
verification code using text (SMS) to the provided phone number.

The cellular carrier's SMS rates apply.

 **Automated Voice Calls**

When Atlas prompts you for a verification code, Atlas calls the provided phone
number. An automated system repeats the 6-digit verification code a total of
three times before hanging up.

The cellular carrier's Voice Call rates apply.

## Important

### Voice only works in the US / Canada.

## Note

Atlas users who operate within a geographic region with limited cellular
service coverage or reliability may encounter delays in receiving the 2FA code
via SMS or Voice. Consider using a 2FA app or device instead.

## Configure Two-Factor Authentication

Text or Voice

2FA App

PIV device

1

### Navigate to the Two-Factor Authentication page.

  1. In the upper right corner of the Atlas UI, click your username to access the Account menu.

  2. Under Atlas, click Two-Factor Authentication.

2

### Enable Two-Factor Authentication.

Click Enable 2FA or __.

When prompted for verification:

  * If you are setting up 2FA, enter your password.

  * If you are editing your 2FA settings, enter a 2FA code.

  * Click Verify.

3

### Configure Voice/SMS Authentication.

  1. Click Primary Method

  2. Click Voice/SMS Number.

  3. In the Enter your phone number box, enter your preferred mobile phone number.

  4. Select your preferred method of receiving codes:

    * Text Message (SMS) _or_

    * Voice Call (US / Canada Only)

  5. Click Verify.

  6. Once you receive the verification code, enter that code into the into the Verify your code boxes. Each digit is entered in its own box.

Atlas automatically verifies the code and saves your settings.

## Configure Backup Two Factor Authentication Phone Number

You can configure a backup phone number for receiving 2FA codes if the primary
method fails or is unavailable.

If you have not yet enabled 2FA for the Atlas account, do so before
proceeding. See Configure Two-Factor Authentication.

1

### Navigate to the Two-Factor Authentication page.

  1. In the upper right corner of the Atlas UI, click your username to access the Account menu.

  2. Under Atlas, click Two-Factor Authentication.

2

### Click __for Two Factor Authentication.

Atlas requires a 2FA verification code to continue.

3

### Configure a backup phone number.

  1. Select Add a Backup Phone.

  2. Enter your preferred phone number in the text entry.

  3. Select your preferred method of receiving codes:

    * Text Message (SMS)

    * Voice Call (US / Canada Only)

  4. Click Verify once you have configured your Voice/SMS authentication settings.

  5. Click Save Changes.

## Generate New Recovery Codes

Atlas can generate single-use recovery codes for use where all other methods
of accessing the account fail. When you generate new recovery codes, you
invalidate previously generated ones.

If you have not yet enabled 2FA for the Atlas account, do so before
proceeding. See Configure Two-Factor Authentication.

1

### Navigate to the Two-Factor Authentication page.

  1. In the upper right corner of the Atlas UI, click your username to access the Account menu.

  2. Under Atlas, click Two-Factor Authentication.

2

### Select the edit button for Two Factor Authentication.

The edit button is __in Atlas.

3

### Select Show Recovery Codes.

## Reset Legacy Two Factor Authentication

If you have legacy 2FA enabled and you lose access to your 2FA device, you can
reset 2FA for your account. Because legacy 2FA is deprecated, you cannot re-
establish it after you reset it. Instead, you can enable multi-factor
authentication.

## Important

The following procedure resets legacy 2FA for your Atlas account. To edit MFA
settings, see multi-factor authentication.

In order to reset your legacy two-factor authentication, you must:

  * Be able to receive email at the address associated with your account.

  * Have the database username and password for a project of which you are a member.

  * Be a direct member of the project which your username and password correspond to. If you have access to the project only through a team that has a role in the project, you cannot reset two-factor authentication for your Atlas account.

  1. Log in to Atlas.

  2. From the 2FA entry dialog, select Reset your two factor authentication.

  3. Select Atlas user? Click here at the bottom of the `Reset Two Factor Authentication` modal.

  4. Enter your Atlas username. Atlas emails a link to the email account associated with the Atlas username.

## Important

The link to start the 2FA reset procedure is only active for two hours after
Atlas sends the email. Make sure you click the link within the two-hour
window.

  5. Click the link in the email to start the 2FA reset procedure.

  6. Follow the directions on the 2FA reset page. After completing the reset procedure, Atlas allows you to log in to the Atlas account without requiring a 2FA code.

← Manage Your Multi-Factor Authentication OptionsAtlas UI Authorization →

