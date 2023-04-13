Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Database User for Your Federated Database Instance

Share Feedback

You must create a database user to access your deployment. For security
purposes, Atlas requires clients to authenticate as MongoDB database users to
access federated database instances.

## Note

If you already created a MongoDB user and added your IP address in your
project's IP access list, you can proceed to Connect Using the MongoDB Shell.

## Procedure

 _Estimated completion time: 2 minutes_

To add a database user to your cluster:

1

### Open the Connect dialog.

Click the Connect button for your federated database instance.

2

### In the Create a MongoDB User step of the dialog, enter a Username and a
Password for your database user.

You'll use this username and password combination to access data on your
cluster.

## Note

If your password contains special characters, you will need to encode them.
For more information, see Special characters in connection string password.

3

### Click Create MongoDB User.

## Tip

### See also:

For information on configuring additional database users on your cluster, see
Configure Database Users.

← Set Up a Private Endpoint for a Federated Database InstanceSet up Self-
Managed X.509 Authentication →

