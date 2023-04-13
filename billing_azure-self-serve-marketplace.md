Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Azure Self-Serve Marketplace

Share Feedback

On this page

  * Link a Azure Billing Account to MongoDB Atlas
  * Unlink an Azure Billing Account from MongoDB Atlas

You can pay for Atlas usage via the Azure Marketplace without any upfront
commitment. You can link an Atlas account to an Azure Billing Account, as well
as delete an existing subscription.

## Link a Azure Billing Account to MongoDB Atlas

To link your Azure Billing Account to MongoDB:

1

### Sign in to your Azure account.

If you do not already have an Azure account, you must create one.

2

### Navigate to the MongoDB Atlas (Pay-as-You-Go) subscription page in the
Azure Marketplace.

3

### Review the Overview, select the Pay as You Go plan from the dropdown, and
click Subscribe.

4

### Complete the steps to subscribe.

  1. Fill out your project details.

  2. Optionally, add key-value tags.

  3. Review your product and plan details.

  4. Click Subscribe.

5

### Wait for Azure to process your subscription.

6

### To complete the subscription process, click Configure account now.

Allow MongoDB to access your Azure information if prompted.

If you are already signed in to an existing MongoDB Atlas account, you are
automatically redirected to the Select an Organization to Link to Your Azure
Billing Account page on the MongoDB Atlas website.

If you are not already signed in to an existing MongoDB Atlas account, you are
prompted to sign in to a MongoDB Atlas account. After you sign in, you are
automatically redirected to the Select an Organization to Link to Your Azure
Billing Account page.

7

### Link an organization.

On the Select an Organization to Link to Your Azure Billing Account page,
click the Link button in the Actions column for the organization you wish to
link to your Azure account. Atlas redirects you to the Billing overview page
of the organization that you are linking with your Azure account.

If you don't have any organizations available to link to your Azure account,
click Create New Organization and follow the steps to create a new
organization.

## Important

If the Link button for a particular organization is dimmed, you can't link the
organization to your Azure account. Mouse over the disabled Link button to
display a tooltip with more information.

8

### Wait for Azure to link your organization.

In the bottom left-hand corner of the Billing page, Atlas displays a pop-up
notifying you that your organization is syncing with your Azure account.
Additionally, the Payment Method field of the Billing page remains empty until
the sync is complete.

When the sync completes successfully, you can see the following in the Atlas
UI:

  * In the bottom left-hand corner of the Billing page, a green pop-up indicates that you have successfully linked your organization to your Azure account.

  * The Payment Method field now shows _Azure Marketplace Subscription_.

## Important

The Edit button in the Payment Method field is dimmed when you have an _Azure
Marketplace Subscription_. To remove the _Azure Marketplace Subscription_
payment method, you must unlink your Azure Billing Account from MongoDB.

## Unlink an Azure Billing Account from MongoDB Atlas

To unlink your Azure Billing Account from MongoDB:

1

### Sign in to your Azure account.

2

### Navigate to your Azure Resource groups.

3

### Navigate to the resource group with your MongoDB (Pay-as-You-Go)
subscription.

4

### Click the _MongoDB Atlas (Pay as You Go)_ subscription that you wish to
unlink.

5

### Click Cancel subscription at the top of the page.

A confirmation modal prompts you to confirm the cancellation of your
subscription.

6

### Click Cancel subscription in the confirmation window.

Upon successful cancellation of your subscription, a notification appears in
the top right corner of your Azure resource group console.

The Overview page of your subscription indicates that you are unsubscribed.

← AWS Self-Serve MarketplaceGCP Self-Serve Marketplace →

