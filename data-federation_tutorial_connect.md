Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect to Your Federated Database Instance

Share Feedback

On this page

  * Prerequisites
  * Connect Using the MongoDB Shell
  * Next Steps

 _Estimated completion time: 15 minutes_

This part of the tutorial will walk you through connecting to your federated
database instance using the MongoDB Shell, `mongosh`.

## Prerequisites

To complete this part of the tutorial, you will need to have completed the
following:

  *  **Part 1:** Deploy a Federated Database Instance

  *  **Part 2:** Configure Connection for Your Federated Database Instance

## Connect Using the MongoDB Shell

Connecting to your federated database instance depends on whether you have the
MongoDB shell, `mongosh`, installed:

Installed

Not Installed

1

### Open the Connect dialog.

Click the Connect button for your federated database instance.

2

### Click Connect with the MongoDB Shell.

3

### Click I have the MongoDB Shell Installed.

4

### Select `mongosh` from the dropdown.

5

### Copy the provided connection string to your clipboard.

This is a unique connection string specific to your federated database
instance. Atlas replaces the `username` of the connection string with the
username of the database user that you created.

6

### Paste and run your connection string in your terminal.

7

### When prompted, enter your database user's password.

You will be prompted to enter the password you specified when you created your
database user in Atlas.

You should now be connected to your federated database instance within the
MongoDB Shell, `mongosh`.

## Important

### Connection Troubleshooting

If you are having trouble connecting to your federated database instance,
double check that you have added your IP address to your IP Access List and
that you are specifying the correct database user credentials. If you have
forgotten your database user credentials, you can always create a new database
user.

## Note

Only one user can authenticate on a connection to a federated database
instance at any given time. If a user authenticates and then runs the
`db.auth()` command, Data Federation replaces the previous user's permissions
with the new user's permissions.

The connectionStatus command shows only the newly authenticated user in the
`authenticatedUsers` output field.

## Next Steps

Now that you're connected to your federated database instance, proceed to
Verify Your Database and Collections.

