Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect to Your Online Archive

Share Feedback

On this page

  * Configure Connection to Online Archive
  * Connect to Online Archive
  * Connect to Online Archive and Cluster
  * Connect to the Federated Database Instance for Your Online Archive

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

You can connect to your Online Archive through the MongoDB Shell. You can get
the connection string for your preferred method of connection from the Atlas
UI.

The connection string determines which data you can access and query. You can
access and query data:

  * In your online archive only.

  * In your online archive and Atlas cluster.

  * In your online archive through your federated database instance.

## Note

Atlas doesn't support LDAP for your Online Archive connection.

Before you connect, you must configure the connection method for your online
archive.

## Configure Connection to Online Archive

You can set up a standard connection or private endpoint for connecting to
your online archives. To set up the connection method:

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Navigate to the Online Archive tab for your cluster.

  1. Click the name of the cluster.

  2. Click the Online Archive tab to view the list of online archives, if any, for the cluster.

3

### Click the Connect button for the Online Archive to which you want to
connect.

4

### Configure your connection type.

To configure the type of connection:

  1. Choose one of the following options:

    * Standard connection

    * Private endpoint

  2. Set up your type of connection. To set up, for:

Standard Connection

Private Endpoint

Click:

    * Add your current IP address to add your current IP address to the list of allowed IP addresses.

    * Add a different IP address to specify the IP address to add to the list of allowed IP addresses.

    * Allow access from anywhere to allow access from all IP addresses.

## Note

If you specify `0.0.0.0` in the IP access list, Atlas accepts all connections
including those over PrivateLink.

5

### Create a database user for your online archive.

To create a database user for your online archive:

  1. Specify Username.

  2. Enter Password or click Autogenerate secure password.

  3. Click Create database uer.

6

### Click Next to get the connection string for your online archive.

## Connect to Online Archive

You can use the connection string for an online archive to access and query
data in your online archive only.

Connect from Clusters Page

Connect from Online Archive Page

To get the connection string from the Database Deployments page:

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Click the Connect button for the cluster.

3

### Choose your connection method.

You can connect through a Driver, Compass, and the MongoDB Shell.

4

### Select Connect to Online Archive to get the connection string for
connecting to your Online Archive.

## Connect to Online Archive and Cluster

You can use the connection string for an online archive and cluster to access
and query data in your online archive and Atlas cluster.

Connect from Clusters Page

Connect from Online Archive Page

To get the connection string from the Database Deployments page:

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Click the Connect button for the cluster.

3

### Choose your connection method.

You can connect through a Driver, Compass, and the MongoDB Shell.

4

### Select Connect to Cluster and Online Archive to get the connection string
for connecting to your cluster and Online Archive.

## Connect to the Federated Database Instance for Your Online Archive

You can use the federated database instance connection string for your online
archive to access and query data in your online archive only.

To get the connection string from the `Data Federation` page:

1

### Navigate to the Data Federation page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Data Federation in the sidebar.

2

### Click the Connect button for the Online Archive to which you want to
connect.

3

### Choose your connection method.

You can connect through a Driver, Compass, and the MongoDB Shell.

4

### Follow the steps in the `Connect` window to get the connection string and
run the connection string in your command line.

← Set Up a Private Endpoint for Online ArchivesManage Online Archives →

