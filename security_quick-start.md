Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Cluster Access with the Quickstart Wizard

Share Feedback

On this page

  * Procedure

The Atlas UI includes a Quickstart page to configure access to your cluster.
To configure access to your cluster, you must do the following:

  * Configure Database Users

  * Configure IP Access List Entries

## Procedure

To configure access to your cluster from the Quickstart page:

1

### Navigate to the Quickstart page.

In the Security section of the left navigation, click Quickstart. If
Quickstart isn't availale in your UI left navigation, add Quickstart to your
UI from your Project Settings page by toggling the Atlas Security Quickstart
to On in the Project Settings page.

2

### Specify how you would like to authenticate the connection to your Atlas
cluster.

In the How would you like to authenticate your connection? section of the
Quickstart page, you can configure one of the following options for your
cluster.

Username and Password

Certificate

  1. Click Username and Password.

  2. Set the new user's Username and Password.

## Note

If you use special characters in your password, you must escape them in the
connection string that you use to connect to your cluster. To learn more, see
Special Characters in Connection String Password.

You can't change a username after you create the user. You can click the Edit
button to edit the password.

  3. Click Create User.

## Tip

### See also:

  * Configure Database Users

  * Set Up Self-Managed X.509 Authentication

3

### Specify from where you would like to connect to your Atlas cluster.

You can enable access for any network that needs to read and write data to
your cluster. To enable access, you can configure access from your local
environment or the cloud environment for your cluster.

Local Environment

Cloud Environment

  1. Choose My Local Environment to add network IP addresses to the project IP Access List. Atlas allows only client connections to the database deployment from entries in the project's IP access list. You can modify the IP addresses in the access list at any time.

  2. Enter the IP address and a description to associate with the IP address in the IP Address and Description fields respectively, or click Add My Current IP Address.

You can specify either a single IP address or a CIDR-notated range of
addresses.

  3. Click Add Entry.

## Tip

### See also:

  * Configure IP Access List Entries

  * Set Up a Network Peering Connection

  * Set Up a Private Endpoint

4

### Click Finish and Close.

Once you have completed setting up database and network access for the first
cluster in your project, Atlas disables access to Quickstart. You can enable
it to revisit these configurations from a consolidated page.

A dialog displays prompting you to specify whether you wish to see the
Quickstart page in your navigation. You can select or deselect the Hide
Quickstart guide in the navigation checkbox to hide or add Quickstart to your
navigation.

Alternatively, you can hide or add Quickstart to your navigation from your
Project Settings page by toggling the Atlas Security Quickstart in the Project
Settings page to Off or On respectively.

5

### Click Go to Database to view your database deployments.

