Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect via `mongosh`

Share Feedback

On this page

  * Prerequisites
  * Connect to Your Database Deployment
  * Troubleshooting

The Connect dialog for a database deployment provides the details to connect
to a database deployment via the MongoDB shell, `mongosh`.

## Prerequisites

### TLS

Clients must support TLS to connect to an Atlas database deployment.

Clients must support the SNI TLS extension to connect to an Atlas `M0` free
cluster or an `M2/M5` shared cluster. MongoDB 4.0 and later shell supports the
SNI TLS extension.

#### IP Access List

To access a database deployment, you must connect from an IP address on the
Atlas project's IP access list. If you need to add an IP address to the IP
access list, you can do so in the Connect dialog. You can also add the IP
address from the Network Access tab.

#### Database User

To access a database deployment, you must create a database user with access
to the desired database(s) on your Atlas database deployment. Database users
are separate from Atlas users. Database users have access to MongoDB
databases, while Atlas users have access to the Atlas application itself.

You can create a database user to access your Atlas database deployment in the
Connect dialog. You can also add the database user from the Database
Deployment view.

## Connect to Your Database Deployment

1

### Click Connect.

  1. Click Database in the top-left corner of Atlas.

  2. In the Database Deployments view, click Connect for the database deployment to which you want to connect.

2

### Choose your Connection Security.

Choose Connection Type from the set of available buttons.

## Note

### Options Display if Feature Enabled

Atlas displays the connection type options after you enable Private IP for
Peering, Private Endpoint, or both. If you haven't enabled either feature, no
buttons display and **Connection Type** defaults to **Standard**.

Standard Connection

Private IP for Peering

Private Endpoint Connection

Use this connection type for allowed public IP addresses.

3

### Choose how you want to limit connections to your database deployment.

Standard Connection

Private IP for Peering

Private Endpoint Connection

Add a Connection IP Address

## Important

Skip this step if Atlas indicates in the Setup connection security step that
you have already configured an IP access list entry in your database
deployment. To manage the IP access list, see Add Entries to the Access List.

Atlas allows standard client connections to the database deployment from
entries in the project's IP access list. The project IP access list differs
from the API access list, which restricts _API_ access to specific IP or CIDR
addresses.

If the IP access list is empty, Atlas prompts you to add an IP address to the
project's IP access list. You can either:

  * Click Add Your Current IP Address to allow access from your current IP address.

  * Click Add an IP Address to add a single IP address or a CIDR-notated range of addresses.

Provide an optional description for the newly added IP address or CIDR range.
Click Add IP Address to add the address to the IP access list.

4

### Create a Database User.

## Important

 **Skip this step** if Atlas indicates in the Setup connection security step
that you have at least one database user configured in your project. To manage
existing database users, see Configure Database Users.

To access the database deployment, you need a MongoDB user with access to the
desired database or databases on the database deployment in your project. If
your project has no MongoDB users, Atlas prompts you to create a new user with
the Atlas Admin role.

  1. Enter the new user's Username.

  2. Enter a Password for this new user or click Autogenerate Secure Password.

  3. Click Create Database User to save the user.

Use this user to connect to your database deployment in the following step.

Once you have added an IP address to your IP access list and added a database
user, click Choose Your Connection Method.

5

### Connect to your Atlas database deployment with `mongosh`.

Select Connect with the MongoDB Shell.

The next screen offers you options to proceed based on whether or not you
already have `mongosh` installed on your system.

I do not have the MongoDB Shell installed

I have the MongoDB Shell installed

Select your OS from the dropdown menu.

Windows

macOS

Linux

  1. Download using one of the following options:

    * Click Download mongosh to begin the download.

    * Click Copy download URL to copy a download URL to your clipboard, then either:

      * Use `curl` to fetch the installer file from the URL, or

      * Paste the URL in a browser window.

    * Download the installer from the MongoDB Shell page.

  2. Extract the files from the downloaded archive.

  3. Add the `mongosh` binary to your `PATH` environment variable.

Ensure that the extracted MongoDB Shell binary is in the desired location in
your filesystem, then add that location to your `PATH` environment variable.

    1. Open the Control Panel.

    2. In the System and Security category, click System.

    3. Click Advanced system settings. The System Properties modal displays.

    4. Click Environment Variables.

    5. Select Path and click Edit.

    6. Click New and add the filepath to your `mongosh` binary.

    7.  _Step 3_ of the Atlas modal displays a copyable connection string. This string includes the name of the MongoDB user that can authenticate with the database deployment. Copy this string. To connect as a different MongoDB user, change the \--username option.

    8. Paste the `mongosh` command and connection string into a terminal. Run the command. The shell prompts you for the password.

## Note

If the input device is not a terminal, `mongosh` doesn't prompt for a
password. Instead, `mongosh` interprets any input on stdin after the
connection string as a password.

## Troubleshooting

If you are experiencing issues connecting to your database deployment, see
Troubleshoot Connection Issues.

← Connect via CompassConnect via BI Connector for Atlas →

