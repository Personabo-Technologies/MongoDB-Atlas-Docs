Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Connection for Your Federated Database Instance

Share Feedback

You must configure the type of connection for your federated database
instance. You can set up a Standard connection or a Private endpoint to
connect to your federated database instance.

For this tutorial, configure a standard connection. To complete this part of
the tutorial, you must first Deploy a Federated Database Instance.

## Procedure

To configure the type of connection:

1

### Open the Connect dialog.

Click the Connect button for your federated database instance.

2

### Choose the type of connection that you wish to configure.

You can choose one of the following options:

  * Standard connection \- to configure this type of connection, you must do the following:

    1. Add Your IP Address to the IP Access List

    2. Create a Database User for Your Federated Database Instance

  * Private endpoint \- to configure this type of connection, you must do the following:

    1. Set Up a Private Endpoint for a Federated Database Instance

    2. Create a Database User for Your Federated Database Instance

## Note

If you specify `0.0.0.0` in your project IP access list, Atlas will accept all
connections including those over PrivateLink.

## Next Steps

Now that you've configured a standard connection, connect to your federated
database instance.

← Deploy a Federated Database InstanceAdd Your IP Address to the IP Access
List →

