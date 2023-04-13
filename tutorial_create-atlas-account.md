Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create an Atlas Account

Share Feedback

On this page

  * Considerations
  * Prerequisites
  * Register a new Atlas Account
  * Log in to Your Atlas Account
  * Create an Atlas Organization and Project
  * Next Steps

 _Estimated completion time: 5 minutes_

Register for an Atlas account using your GitHub account, your Google account
or your email address.

## Considerations

To register with and log in to Atlas, you can use one -- and only one -- of
the following options:

  * Your email account

  * Your GitHub account

  * Your Google account

## Note

If your company uses Federated Authentication, you must use your company email
address.

### GitHub Accounts

If you register with your GitHub Account, the following differences apply when
using your GitHub account with Atlas:

  * GitHub manages your user details, email address, and password. You can't change this information using the Atlas console or API.

  * GitHub manages your 2FA. You can't use Atlas multi-factor authentication and won't be prompted for an Atlas 2FA verification when you log into Atlas. GitHub should verify your identity using GitHub 2-Step Verification.

  * If you linked your Atlas account to your GitHub Account, you can unlink these accounts in Atlas.

### Google Accounts

If you register with your Google Account, the following differences apply when
using your Google account with Atlas:

  * Google manages your user details, email address, and password. You can't change this information using the Atlas console or API.

  * Google manages your 2FA. You can't use Atlas multi-factor authentication and won't be prompted for an Atlas 2FA verification when you log into Atlas. Google should verify your identity using Google 2-Step Verification.

  * If you linked your Atlas account to your Google Account, you can unlink these accounts in Atlas.

### MongoDB Cloud Manager Users

If you use MongoDB Cloud Manager, use your Cloud Manager credentials to log in
to Atlas. You can then create a new Atlas project from Cloud Manager.

## Prerequisites

### Add the Atlas CDN Host to your Allow List

Atlas uses a CDN to serve content quickly. If your organization uses a
firewall, add the following Atlas CDN host to the firewall's allow list to
prevent issues accessing the Atlas UI: `https://assets.mongodb-cdn.com/`.

### GitHub Accounts Require a Public Email Address

If you try to register with Github, you must have an public email address
associated with your GitHub account. Atlas returns an error if you attempt to
register without a public email address.

To set a public GitHub email address:

  1. After you log into GitHub, click Settings on your profile menu. Your Public Profile page should display.

  2. Select one email address from the Public email dropdown in your Public Profile.

If GitHub greys out this dropdown menu:

    1. Click Emails from the left-side menu.

    2. Clear the Keep my email addresses private box.

    3. Return to the Public Profile page and select an email address from the Public email dropdown.

  3. Click Update profile to save the changes.

## Register a new Atlas Account

Select a tab based on how you would like to register your account:

Atlas CLI

Atlas UI

To register with Atlas using the Atlas CLI, run the following command:

    
    
    atlas auth register [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas auth register.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Note

If you run `atlas setup` with the default selections, you don't need to run
`atlas auth register`.

## Log in to Your Atlas Account

Select a tab based on how you would like to log in:

Atlas CLI

Atlas UI

To authenticate with Atlas using the Atlas CLI, run the following command:

    
    
    atlas auth login [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas auth login.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

For step-by-step instructions on logging in using the Atlas CLI, see Connect
from the Atlas CLI.

## Create an Atlas Organization and Project

Create an Atlas organization and then create a project in this organization.
You will deploy your first cluster in this project.

## Next Steps

With your Atlas account, open the organization and its project, and then
proceed to Deploy a Free Cluster.

## Tip

### See also:

To learn about shortcuts you can use to navigate your new Atlas account, see
Atlas Goto.

