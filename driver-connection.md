Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect via Your Application

Select your language

C

On this page

  * Prerequisites
  * Connect Your Application
  * Driver Examples
  * Troubleshooting

The Connect dialog for a database deployment provides the details to connect
to a database deployment with an application using a MongoDB driver.

## Note

Serverless instances don't support connecting via certain drivers or driver
versions at this time. To learn more, see Serverless Instance Limitations.

## Prerequisites

C

C++11

C#

Go

Java (Sync)

Node.js

Perl

PHP

Python

Ruby

Rust (Async)

Rust (Sync)

Scala

Swift (Async)

Swift (Sync)

### Driver Version

Your driver version must be compatible with your version of the MongoDB
server. We recommend choosing the latest driver that is compatible with your
MongoDB server version to use the latest database features and prepare for
future version upgrades.

For a list of driver versions that contain the full set of functionality for
your version of the MongoDB server, check the compatibility matrix for your
MongoDB driver.

For a list of driver versions that you can use to connect to serverless
instances, see Minimum Driver Versions for Serverless Instances.

## Important

When you upgrade your driver version, some commands, methods or options may be
deprecated and removed. Check your MongoDB driver API documentation to ensure
a smooth transition.

Applications running with 4.0-series drivers will work with MongoDB database
deployments running MongoDB 4.4 as long as:

  * The drivers recommended for MongoDB 4.4 in the driver compatibility matrices are tested against MongoDB 4.4. Check the MongoDB driver documentation page for the driver compatibility matrix for your language.

  * No functionality new to MongoDB 4.2, or MongoDB 4.4 is being used, and

  * No commands, methods, or options removed in MongoDB 4.2 (including `db.collection.geoNear()`, `db.collection.group()`, and `db.eval()`), or MongoDB 4.4 are being used, and

  * Other compatibility changes in MongoDB 4.4 to `projections` (including `$slice projections`), `$sort`, `text search`, and `mapReduce` do not impact them.

We recommend using MongoDB 4.4-series drivers with MongoDB 4.4 to use newer
database features and prepare for future version upgrades.

### Optimized Connection Strings for Sharded Clusters Behind a Private
Endpoint

To connect to your sharded cluster using a driver and an optimized connection
string, you must use at least one of the following driver versions:

Driver

|

Version  
  
|  
  
C

|

1.19.0  
  
C++

|

3.7.0beta1  
  
C#

|

2.13.0  
  
Go

|

1.6.0  
  
Java

|

4.3.0  
  
Motor

|

2.5.0  
  
Node.js

|

4.1.0  
  
PHP

|

1.11.0 (Extension)

1.10.0 (Library)  
  
PyMongo

|

3.12.0  
  
Ruby

|

2.16.0  
  
Rust

|

2.1.0  
  
Scala

|

4.3.0  
  
Swift

|

1.2.0  
  
### TLS

Clients must support TLS to connect to an Atlas database deployment.

Clients must support the SNI TLS extension to connect to an Atlas `M0` free
cluster or `M2/M5` shared cluster. To verify that your MongoDB driver supports
the SNI TLS extension, refer to the Compatibility section of your driver's
documentation. If the driver is compatible with MongoDB 4.2 and later, it
supports the SNI TLS extension.

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

## Connect Your Application

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

### Select Connect your application.

In the Choose a connection method step, select Connect your application.

6

### Select Your Driver and Version.

Select your driver and version from the dropdown menus. The code sample
containing a connection string displays.

  * Replace `<password>` with the password specified when you created your database user.

  * Replace `<myFirstDatabase>` with the name of the database that connections will use by default. If you omit the database, the `test` database is used by default. If you configured the user on a different database, specify that database in the connection string.

## Note

If your passwords, database names, or connection strings contain reserved URI
characters, you must escape the characters. For example, if your password is
`@bc123`, you must escape the `@` character when specifying the password in
the connection string, such as `%40bc123`. To learn more, see Special
Characters in Connection String Password.

To learn more, see Driver Compatibility.

## Driver Examples

In this example URI connection strings, the user `kay` provides their password
`myRealPassword` to authenticate and connect to an Atlas database deployment.

Select your driver from the following options:

C

C++11

C#

Go

Java (Sync)

Node.js

Perl

PHP

Python

Ruby

Rust (Async)

Rust (Sync)

Scala

Swift (Async)

Swift (Sync)

## Note

To connect to an Atlas `M0` free cluster or `M2/M5` shared cluster, you must
use a C driver version that supports MongoDB 4.0 and later. For complete
documentation on compatibility between the C driver and MongoDB, see the
MongoDB compatibility matrix. We recommend that you upgrade to the latest
version of the driver.

    
    
    client = mongoc_client_new ("mongodb+srv://kay:myRealPassword@cluster0.mongodb.net/?serverSelectionTryOnce=false&serverSelectionTimeoutMS=15000&w=majority");  
      
    db = mongoc_client_get_database (client, "test");  
  
C

MongoDB Version

|

Recommended Driver Version(s)  
  
|  
  
All

|

See the MongoDB compatibility matrix for the latest recommended driver
versions.  
  
MongoDB 4.2 and later

|

Version 1.11 and later.  
  
### Behavior

## Note

The following configuration options only apply if running the C driver in
single-threaded mode.

MongoDB drivers automatically attempt server selection following a cluster
election or failover event. By default, the C driver immediately raises an
error if its first attempt to select a server fails. The following
configuration settings may improve application connectivity to an Atlas
cluster at the expense of spending more time in a server selection loop:

  * Set serverSelectionTryOnce to `false` to direct the C driver to perform server selection up to the time limit defined by `serverSelectionTimeoutMS`.

  * Lower the serverSelectionTimeoutMS to `15000` from the default of `30000`. MongoDB elections typically take 10 seconds, but can be as fast as 5 seconds on Atlas. Setting this value to 15 seconds (`15000` milliseconds) covers the upper bound of election plus additional time for latency.

## Troubleshooting

If you are experiencing issues connecting to your database deployment, see
Troubleshoot Connection Issues.

## Tip

### See also:

Connection Limits and Cluster Tier

← Connect to a Database DeploymentConnect via Compass →

