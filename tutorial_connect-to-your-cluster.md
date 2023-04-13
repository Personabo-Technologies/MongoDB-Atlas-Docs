Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect to Your Cluster

Share Feedback

On this page

  * Prerequisites
  * Download and Install Utility
  * Connect to Your Atlas Cluster
  * Next Steps

 _Estimated completion time: 5 minutes_

You can connect to your cluster in a variety of ways. This tutorial describes
how to connect to your cluster using the `mongosh`, the Node.js driver, the
PyMongo driver, and Compass.

## Prerequisites

  * An Atlas account.

  * An organization and project added with an account's user who has permissions to create clusters in this account.

  * An active cluster created in this account.

  * An IP address added to your IP access list.

  * A Database user on your cluster.

See Parts 1 - 4 of this tutorial for help with the prerequisites.

## Note

You must have a database user set up on your cluster to access your
deployment. For security purposes, Atlas requires clients to authenticate as
database users to access clusters.

## Download and Install Utility

The following steps show you how to download and install the `mongosh`, the
Node.js driver, and the PyMongo driver.

Before you start, verify that you have met all prerequisites.

Select the appropriate tab based on how you would like to connect to your
cluster:

PyMongo Driver

Node.js Driver

MongoDB Shell

Compass

MongoDB drivers allow you to communicate with your MongoDB database
programatically.

For this tutorial, we will walk through setting up and using the Python
MongoDB driver, called PyMongo. If you are interested in working with a
different driver, refer to the MongoDB Driver documentation.

To complete this tutorial you must have:

  * A terminal.

  * Python. Visit the Python Downloads Page and download the latest version of Python for your operating system.

  * The pip package installer. Starting with Python 2.7.9 and Python 3.4, packages downloaded from https://python.org include `pip`. To install `pip` manually, see the pip installation page. This package includes Python.

  * The PyMongo driver.

  * A text editor.

Once you have Python and `pip` installed:

1

### Open your terminal.

2

### Install the PyMongo Driver.

Run the following command in your terminal:

    
    
    python -m pip install "pymongo[snappy,gssapi,srv,tls]"  
      
  
This command installs the PyMongo driver and a few dependencies for the
driver. To learn more, see the Python Driver Installation Page on GitHub.

3

### Test your PyMongo installation.

Test your PyMongo installation to ensure you can successfully connect to your
cluster.

  1. Run the following command to open the Python shell:
    
        python  
      
  
  2. Import PyMongo by running the following command in the Python shell:
    
        import pymongo  
      
  
  3. Check your PyMongo version using the following command:
    
        pymongo.version  
      
  
If PyMongo is correctly installed, you should see an output similar to the
following:

    
        '3.11.0'  
      
  

## Connect to Your Atlas Cluster

In Atlas, you can connect to your cluster using the following connection
methods:

  * Connect with the MongoDB Shell to interact with your cluster using the Javascript interface of `mongosh`.

  * Connect your application to your cluster using the Node.js driver, or the PyMongo driver.

  * Connect to your cluster using MongoDB Compass to explore, modify, and visualize your data with Compass.

Before you start, verify that you have met all prerequisites.

Select the appropriate tab based on your preferred connection method:

PyMongo Driver

Node.js Driver

MongoDB Shell

Compass

 _Estimated completion time: 5 minutes_

You'll need to get your cluster's connection string from Atlas to connect to
the cluster using the PyMongo driver.

1

### Click Connect.

  1. Click Database in the top-left corner of Atlas.

  2. In the Database Deployments view, click Connect for the database deployment to which you want to connect.

2

### Click Choose a connection method.

3

### Click Connect your application.

The Driver dropdown opens. In it, you can select the driver type and version.

4

### Select `Python` and your version of the driver.

The connection string displays.

5

### Copy the provided connection string.

6

### Configure the provided connection string.

  * Replace `<password>` with the password specified when you created your database user.

  * Replace `<myFirstDatabase>` with the name of the database that connections will use by default. If you omit the database, the `test` database is used by default. If you configured the user on a different database, specify that database in the connection string.

## Note

If your passwords, database names, or connection strings contain reserved URI
characters, you must escape the characters. For example, if your password is
`@bc123`, you must escape the `@` character when specifying the password in
the connection string, such as `%40bc123`. To learn more, see Special
Characters in Connection String Password.

7

### Import MongoClient from PyMongo.

To connect to a running MongoDB instance, PyMongo requires `MongoClient`. In
the Python shell running in your terminal, run the following command to import
`MongoClient`:

    
    
    from pymongo import MongoClient  
      
  
8

### Connect to your cluster.

Create the command that specifies a client for connecting to your cluster.

  1. In your Python shell, paste your updated connection string from the text editor into this command:
    
        client = MongoClient('<your updated connection string>')  
      
  
  2. Update the connection string with your database user password.

  3. Verify that you have enclosed the connection string in single quotes.

  4. Run the resulting command. It specifies a client that will connect to your cluster.

  5. Connect to your cluster using this client.

## Next Steps

Now that you are connected to your cluster, proceed to Insert and View Data in
Your Cluster.

