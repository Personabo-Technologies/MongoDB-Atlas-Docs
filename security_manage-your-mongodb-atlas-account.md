Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Your MongoDB Atlas Account

Share Feedback

On this page

  * Find Your MongoDB Atlas Account
  * Change Your Atlas Email Address
  * Unlink Your MongoDB Atlas Account from Your GitHub Account
  * Unlink Your MongoDB Atlas Account from Your Google Account
  * Delete an Atlas Account

## Find Your MongoDB Atlas Account

You can manage your Atlas account's settings, unlink your account from your
Google or GitHub account, and configure multi-factor authentication for your
Atlas account.

To find your MongoDB Atlas account:

1

### Click your account's name in the Atlas top menu.

2

### Click Manage your MongoDB Account.

The Overview page opens. From here, you can:

  * Access the MongoDB Atlas login page.

  * Access Support to view active support cases and speak to the Support team.

  * Visit the MongoDB University to take free courses to become a certified expert on MongoDB.

  * Visit the MongoDB Community Forums to meet other MongoDB developers.

From the left-side navigation bar, you can also:

  * Provide your personal information in Profile Info.

    * If you manage your account through your Google Account, visit your Google Account to manage your personal information.

    * If you manage your account through your GitHub Account, visit your GitHub Account to manage your personal information.

  * Unlink your Mongodb Atlas account from Google or GitHub in Profile Info.

  * Manage Your Multi-Factor Authentication Options in Security.

## Change Your Atlas Email Address

You can change the email address that you use to log in to your MongoDB Atlas
account.

## Note

If your login information is managed by an identity provider with Federated
Authentication, contact your company's administrator instead.

If you log in with Google SSO, you must unlink your account before you change
your email address.

To change your email address:

1

### Click your account's name in the Atlas top menu.

2

### Click Manage your MongoDB Account.

3

### Click Profile Info in the navigation bar.

4

### Change your email address.

  1. Click Change Email Address under your current email address.

  2. Enter your password. If you have MFA enabled, authenticate with your MFA method.

  3. Enter a new email address.

## Note

You can't use an email address associated with another account or with a
deleted account.

  4. Click Save Changes.

## Note

After you save your changes, a banner at the top of the page asks you to
verify your email. If you want to cancel your change and continue using your
original email address, click Cancel Request on the banner.

5

### Confirm your new email account.

A verification email is sent to your new email address once you save your
changes. In that email, click Verify Email to update your email address. The
project activity feed records your update.

6

### Log in to Atlas.

Use your updated email address to log in to Atlas.

## Unlink Your MongoDB Atlas Account from Your GitHub Account

If you linked your MongoDB Atlas account to your Github Account, you can
unlink it using the following procedure.

To unlink your MongoDB Atlas account from your Github Account:

1

### Unlink your account from the GitHub acccount.

  1. Click Manage your MongoDB Account.

  2. Click Profile Info. The console indicates that:

    * Your Atlas account is linked to your GitHub account.

    * If you intend to unlink your account, you must change your password for your Atlas account.

  3. Click Unlink from GitHub.

  4. Click Confirm. Atlas sends you an email to your email account. This message has instructions to reset your Atlas account password.

2

### Reset your password.

  1. Log in to email and locate the Password Reset email.

## Note

If you don't reset your password within two hours, submit a new request.

  2. Click the password reset link in the email to complete the password reset process.

  3. Type your email.

  4. Type your new Atlas password.

## Note

### Atlas Password Policy

Your Atlas **user account** password must:

    * Contain at least eight characters.

    * Contain unique characters, numbers, or symbols.

    * Exclude your email address and Atlas username.

    * Differ from your previous four passwords.

    * Differ from the most commonly used passwords.

  5. Retype your new password to confirm it.

  6. Click Save. When your password meets the requirements and matches in both fields, you have reset your password. Atlas displays a success message with a link to log in.

3

### Log in to Atlas.

  1. Click Log in to continue.

  2. Type your email.

  3. Type your new password.

## Unlink Your MongoDB Atlas Account from Your Google Account

If you linked your MongoDB Atlas account to your Google Account, you can
unlink it using the following procedure.

To unlink your MongoDB Atlas account from your Google Account:

1

### Unlink your account from the Google acccount.

  1. Click Manage your MongoDB Account.

  2. Click Profile Info. The console indicates that:

    * Your Atlas account is linked to your Google account.

    * If you intend to unlink your account, you must change your password for your Atlas account.

  3. Click Unlink from Google.

  4. Click Confirm. Atlas sends you an email to your Gmail account. This message has instructions to reset your Atlas account password.

2

### Reset your password.

  1. Log in to Gmail and locate the Password Reset email.

## Note

If you don't reset your password within two hours, submit a new request.

  2. Click the password reset link in the email to complete the password reset process.

  3. Type your email.

  4. Type your new Atlas password.

## Note

### Atlas Password Policy

Your Atlas **user account** password must:

    * Contain at least eight characters.

    * Contain unique characters, numbers, or symbols.

    * Exclude your email address and Atlas username.

    * Differ from your previous four passwords.

    * Differ from the most commonly used passwords.

  5. Retype your new password to confirm it.

  6. Click Save. When your password meets the requirements and matches in both fields, you have reset your password. Atlas displays a success message with a link to log in.

3

### Log in to Atlas.

  1. Click Log in to continue.

  2. Type your email.

  3. Type your new password.

## Delete an Atlas Account

This section walks you through deleting your Atlas account.

### Prerequisites

To delete your Atlas account, you must ensure that you have no:

  * Outstanding invoices

  * Active database deployments

  * Projects

  * Organizations

## Important

If you log in to Atlas through an identity provider, you can't delete your
account yourself. Contact your identity provider to delete your Atlas account.

If you use legacy two-factor authentication, disable it before proceeding to
delete your Atlas account.

### Delete All Projects

#### Delete a Project

To delete a project for an organization:

  * You must either have the `Owner` role for the project or have the `Organization Owner` role for the project's organization.

  * The project must have no outstanding invoices.

  * The project must have no active database deployments. To learn how to view your project's invoices, see Manage Invoices.

##### Terminate All Clusters

## Warning

Terminating a cluster also deletes any backup snapshots for that cluster. See
Snapshot Schedule.

To terminate an Atlas cluster:

1

###### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

###### If you enabled termination protection, disable it.

  1. Next to the cluster you want to terminate, click __.

  2. Click Edit Configuration.

  3. Click Additional Settings and set the Termination Protection toggle to off.

  4. Click Review Changes.

  5. Click Apply Changes.

3

###### Click __next to the cluster you want to terminate.

4

###### (Optional) Keep existing snapshots after termination.

If you have a Backup Compliance Policy enabled and you terminate a cluster,
Atlas automatically maintains all existing snapshots after the termination
according to the backup policy. Atlas retains the oplog for restoring a point
in time with continuous cloud backup in a static state until Atlas can no
longer use them for continuous cloud backup.

Otherwise, if you have Cloud Backup enabled, you can toggle Keep existing
snapshots after termination to On.

If you have Cloud Backup disabled, this option is unavilable.

5

###### Click Terminate.

To terminate an Atlas serverless instance:

1

###### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

###### If you enabled termination protection, disable it.

  1. Next to the serverless instance you want to terminate, click __.

  2. Click Edit Configuration.

  3. Click Additional Settings and set the Termination Protection toggle to off.

  4. Click Review Changes.

  5. Click Apply Changes.

3

###### Click __next to the serverless instance you want to terminate.

4

###### Click Terminate.

Atlas executes the terminate operation after completing any in-progress
deployment changes.

##### Delete the Project

You can delete a project for an organization either from the organization's
Projects view or the project's Project Setting view:

Delete from Projects view

Delete from Project Setting view

1

###### View all of your projects.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. Click the Leaf icon in the upper left corner of the page. You can also expand the Projects menu in the navigation bar, then click View All Projects.

2

###### For the project you want to delete, click __.

3

###### Click Delete Project.

4

###### If Legacy Two-Factor Authentication is enabled, enter the verification
code.

After verifying, click Delete Project again.

### Leave or Delete All Organizations

#### Leave an Organization

## Note

If you are the only `Organization Owner` in an organization, you must promote
another member to `Organization Owner` before you can leave an organization.

1

##### View all of your organizations.

  1. Expand the Organizations menu in the navigation bar.

  2. Click View All Organizations.

2

##### Leave organization.

For the organization you wish to leave, click its Leave button to bring up the
Leave Organization dialog.

3

##### Click Leave Organization in the Leave Organization dialog.

#### Delete an Organization

## Note

To delete an organization, you must have the `Organization Owner` role for the
organization.

You cannot delete an organization that has active projects. You must delete
the organization's projects before you can delete the organization.

1

##### Navigate to the Settings page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click the Organization Settings icon next to the Organizations menu.

2

##### In the General Settings tab, click Delete.

This displays the Delete Organization dialog.

3

##### Click Delete Organization to confirm.

Once you delete all active database deployments, projects, and organizations,
you are no longer billed for any Atlas activity and no longer receive Atlas
alerts.

### Delete your Atlas Account

## Important

Once you delete your account there's no way to recover it.

You can't reuse the email address that is associated with the deleted account
to create a new Atlas account.

1

#### Navigate to your Profile Info.

  1. Click your name in the top right corner of the Atlas UI.

  2. Click Manage your MongoDB Account.

  3. Click Profile Info in the left navigation panel.

2

#### Click Delete Account.

3

#### Confirm that you want to delete your account.

  1. Acknowledge the implications of deleting your Atlas account.

  2. Click Confirm Account Deletion.

## Note

If there are any requirements you have not yet met, you are prompted to
complete them before deleting your account.

4

#### Verify your identity.

You are prompted to verify your identity:

  * If you use MFA, you are prompted verify your identity with your chosen MFA authentication method.

  * If you use Google SSO, MongoDB sends a code to your email address. Use that code to verify your identity. Accounts that use Google SSO are automatically unlinked as part of the account deletion process.

  * If you don't have MFA configured and don't use Google SSO, you are prompted to re-verify your password. Then, MongoDB sends a code to your email address. Use that code to finish verifying your identity.

Your account is deleted.

← View Activity FeedConfigure MongoDB Support Access to Atlas Backend
Infrastructure →

