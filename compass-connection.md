Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect via Compass

Share Feedback

On this page

  * Prerequisites
  * Connect to Your Database Deployment
  * Troubleshooting

The Connect dialog for a database deployment provides the details to connect
to a database deployment using Compass.

## Prerequisites

### TLS

Use MongoDB Compass 1.5 or later to connect to Atlas database deployments.
These versions support the required SNI TLS extension.

### MongoDB Compass

To complete this procedure, do one of the following:

  * Install MongoDB Compass. See Compass Installation.

  * Upgrade to the latest version of MongoDB Compass by downloading MongoDB Compass from links in the Atlas Connect dialog. To access these links, click Connect for the database deployment you wish to connect to, then click Connect with MongoDB Compass.

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

Compass 1.8 and later

Compass 1.7 or earlier

Use the following procedure to connect MongoDB Compass 1.8 or later versions
to your Atlas database deployment.

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

### Get the Connection String for MongoDB Compass from Atlas.

  1. Click I have MongoDB Compass.

  2. Choose your version of MongoDB Compass in the dropdown. To check the version of MongoDB Compass that you have installed on your system, click About MongoDB Compass in the application.

  3. Copy the connection string presented in the Atlas Connect dialog.

6

### Open MongoDB Compass and Connect to Atlas.

Paste Connection String

Fill in Connection Fields Individually

Use the copied connection string for connecting to MongoDB Compass if your
deployment uses a single cloud provider or doesn't use any of the following:
SSL, authentication certificates, or an SSH tunnel.

  1. Click New Connection and paste the connection string into the Paste your connection string field.

  2. ( _Optional_ ) To save this connection for future use, click Create Favorite and add a name for this connection. You can find saved favorite connections under Favorites in the left pane of the MongoDB Compass Connect window.

  3. Click Connect.

## Troubleshooting

If you are experiencing issues connecting to your database deployment, see
Troubleshoot Connection Issues.

← Connect via Your ApplicationConnect via `mongosh` →

