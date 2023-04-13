Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# AWS Self-Serve Marketplace

Share Feedback

On this page

  * Link an AWS Billing Account to MongoDB Atlas
  * Unlink an AWS Billing Account from MongoDB Atlas

Atlas supports paying for usage via the AWS Marketplace (AWS MP) without any
upfront commitment. You can link an Atlas account to an AWS Billing Account,
as well as delete an existing subscription.

## Link an AWS Billing Account to MongoDB Atlas

To link your AWS Billing Account to MongoDB:

1

### Sign in to your to AWS account.

If you do not already have an AWS account, create a new AWS account.

2

### Navigate to the AWS Marketplace (AWS MP).

3

### Search for _MongoDB Atlas (Pay as You Go)_ in the search bar.

4

### In the displayed search results, select _MongoDB Atlas (Pay as You Go)_.

## Important

Do not select _MongoDB Atlas for AWS_.

5

### On the MongoDB Atlas product overview page, click Continue to Subscribe.

6

### On the MongoDB Atlas (Pay As You Go) page, click Subscribe.

7

### In the modal, click the yellow Set Up Your Account button.

If you are already signed in to an existing MongoDB Atlas account, you are
automatically redirected to the Select an Organization to Link to Your AWS
Billing Account page on the MongoDB Cloud Atlas website when you click Set Up
Your Account.

If you are not already signed in to an existing MongoDB Atlas account, you are
prompted to sign in to a MongoDB Atlas account. Upon successful sign-in, you
are automatically redirected to the Select an Organization to Link to Your AWS
Billing Account page.

## Note

If you are unable to complete your registration, you can return to this step
by navigating to the Manage Subscriptions page in the AWS Marketplace.

8

### On the Select an Organization to Link to Your AWS Billing Account page,
link an organization.

On the Select an Organization to Link to Your AWS Billing Account page, click
the Link button in the Actions column of the organization you wish to link
your AWS account to. You are redirected to the Billing overview page of the
organization that you are linking your AWS account to.

If you do not have any organizations available to link your AWS account to,
create a new organization.

## Important

If the Link button for a particular organization is disabled, the organziation
is unable to be linked to your AWS account. To see why you are unable to link
a particular organziation, mouse over the disabled Link button to display a
tooltip with more information.

9

### Wait for AWS to finish syncing your organization.

In the bottom left-hand corner of the Billing page, a pop-up notifying you
that your organization is being synced with your AWS account is displayed.
Additionally, the Payment Method field of the Billing page remains empty until
the sync is complete.

Upon successful sync, a green pop-up in the bottom left-hand corner of the
Billing page displays, indicating that you have successfully linked your
organization to your AWS account. In addition, _AWS Marketplace Subscription_
is now listed in the Payment Method field.

## Important

The Edit button in the Payment Method field is disabled when you have an _AWS
Marketplace Subscription_. To remove the _AWS Marketplace Subscription_
payment method, you must unlink your AWS Billing Account from MongoDB.

## Unlink an AWS Billing Account from MongoDB Atlas

To unlink your AWS Billing Account from MongoDB:

1

### Sign in to your to AWS account.

If you do not already have an AWS account, create a new AWS account.

2

### Navigate to the AWS Marketplace (AWS MP).

3

### Navigate to the Manage Subscriptions page.

4

### Select the _MongoDB Atlas (Pay as You Go)_ subscription that you wish to
unlink.

The information for the selected subscription is displayed.

5

### Click the Actions button in the Agreement section.

A dropdown with available actions is displayed.

6

### In the dropdown, click Cancel Subscription.

## Important

Cancelling your subscription unlinks your AWS billing account from MongoDB but
does **not** delete your resources or data. You will continue to incur charges
for your MongoDB resources and data after you unlink your AWS billing account.
To manage billing through MongoDB, see Manage Billing. To delete your Atlas
resources and data, see Delete an Atlas Account.

A modal asking you if you are sure you want to cancel your subscription
displays. If you wish to cancel your subscription, select the checkbox, then
click Yes, cancel subscription. Upon successful cancellation of your
subscription, a green banner displays at the top of the Manage Subscriptions
page.

If you do not wish to cancel, click No, don't cancel.

← Online Archive CostsAzure Self-Serve Marketplace →

