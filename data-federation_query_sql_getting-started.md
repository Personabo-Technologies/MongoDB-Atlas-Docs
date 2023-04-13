Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Started

Share Feedback

On this page

  * Prerequisites
  * Create a Federated Database Instance
  * Install Client Software
  * Connect to Your Federated Database Instance
  * Run SQL Queries

## Note

### Preview

The support for SQL queries is available as a Preview feature. This feature
and the corresponding documentation may change at any time during the Preview
phase.

This page guides you through setting up a federated database instance with
sample data. You can then run SQL queries against the sample data using the
MongoDB JDBC Driver.

## Prerequisites

  * A MongoDB database user with which to connect.

## Create a Federated Database Instance

To create a federated database instance and map it to the sample data:

1

### Navigate to the Data Federation dashboard in Atlas.

Select Data Federation from the left navigation panel.

2

### Click Create Federated Database Instance.

If you have an existing federated database instance, instead click Create
Federated Database in the top right corner of the dashboard.

3

### Under Data Sources, select AWS S3.

You can use a sample dataset to start exploring Atlas SQL through Atlas Data
Federation without configuring a data source yourself.

## Tip

### Configure Data Sources

To learn more about configuring different types of data sources, see Define
Data Stores for a Federated Database Instance.

If you want to configure data from a Atlas cluster, you must use MongoDB
version 5.0 or greater for that cluster to take advantage of Atlas SQL.

4

### Add sample data to your federated database instance.

Expand the S3 store `sample-data-atlas-data-lake` if it isn't expanded
already.

For this tutorial, configure your federated database instance as follows using
the Federated Database Instance panel:

1

#### Rename the default collection.

Click __next to the default collection`Collection0` to edit its name. For this
tutorial, rename your collection `Sessions`.

2

#### Create a second collection.

Click __next to the default name`Database0` to add a collection to the
database. For this tutorial, name your new collection `Users`.

3

#### Add data to your virtual database.

Drag and drop the following data sources into the respective federated
database instance virtual collections:

  * `/mflix/sessions.json`, into the `Sessions` collection, and

  * `/mflix/users.json` into the `Users` collection.

5

### Click Save.

Your federated database instance displays a success message.

To learn more about configuring Atlas Data Federation with real data stores,
see Define Data Stores for a Federated Database Instance.

## Install Client Software

Install the following client software to connect to and query your sample data
with SQL.

1

### Install DBeaver

DBeaver is a free, universal database tool. You can use it to explore your
sample data in this tutorial. Download and install DBeaver (Community
Edition).

2

### Install JDBC Driver

Download the latest MongoDB JDBC Driver version.

## Important

To connect with the Atlas SQL interface, you must do the following:

  * Use MongoDB JDBC driver version 2.0.0 or later.

  * Download the `all.jar` file, which includes necessary driver classes and dependencies.

## Connect to Your Federated Database Instance

To connect to your federated database instance from DBeaver:

1

### Navigate to your federated database instance.

If it isn't already displayed, select Data Federation from the left navigation
panel.

2

### Click Connect to open the federated database instance connection modal.

3

### Select Connect using the Atlas SQL Interface.

4

### Select JDBC Driver.

## Note

This tutorial uses the JDBC Driver to connect. See Connect for alternative
connection methods.

5

### Copy your connection information.

Atlas Data Federation provides a connection string to connect to your
federated database instance. You'll need this in a later step.

6

### Connect from DBeaver.

1

#### Launch DBeaver.

2

#### Add a new driver.

  1. In DBeaver, click Database and select Driver Manager from the dropdown menu.

  2. Click New to open the Create new driver modal.

  3. In the Settings tab, enter the following information:

|  
  
|  
  
Driver Name

|

`MongoDB`  
  
Class Name

|

`com.mongodb.jdbc.MongoDriver`  
  
  4. In the Libraries tab, click Add File and add your JDBC driver `all.jar` file.

Click Find Class.

  5. Click OK. The Create new driver modal closes.

3

#### Create a database connection.

  1. In DBeaver, click Database and select New Database Connection from the dropdown menu to open the Connect to a database modal.

  2. From the list of databases, select the `MongoDB` database driver that you created in the previous step.

## Tip

If you don't see `MongoDB`, select the All category inside the modal.

Click Next.

  3. In the Main tab, enter the following information:

|  
  
|  
  
JDBC URL

|

Your connection string from step 5.  
  
Username

|

The MongoDB user to connect with.  
  
Password

|

The MongoDB user's password.  
  
  4. In the Driver properties tab, expand User Properties. Add the following key-value properties:

|  
  
|  
  
database

|

The name of your virtual database.  
  
user

|

The MongoDB user to connect with. Not required if you entered a `Username` in
the previous step.  
  
password

|

The MongoDB user's password. Not required if you entered a `Password` in the
previous step.  
  
## Tip

If you created your first virtual database during this tutorial, your
database's name is `Database0`. Otherwise, find your virtual database's name
in your Atlas SQL federated database instance interface under the Data
Federation tab.

4

#### Click Finish.

7

###  _(Optional)_ Confirm that sample can be accessed from your federated
database instance.

In the Database Navigator, expand your MongoDB connection to verify that the
sample data that the federated database instance store is mapped to is
accessible.

To learn more about the different methods you can use to connect to a
federated database instance, see Connect.

## Run SQL Queries

To run SQL queries in DBeaver:

1

### Expand your MongoDB connection.

The DBeaver Database Navigator displays your virtual databases.

2

### Open a SQL console.

  1. Right-click the virtual database you want to query.

  2. Select SQL Editor.

  3. Select Open SQL console.

A new SQL console window opens connected to the virtual database you selected.

3

### Enter a SQL query in the console.

4

### Click Execute SQL Statement to run your SQL query.

If the query is successful, Atlas SQL displays the results in a table view
below your query.

### Example SQL Queries

Try running the following SQL queries against the sample data in your
federated database instance.

## Note

These examples reference data that we suggest that you add in this tutorial.
If you are using different data, modify these queries for your namespaces.

### SELECT Statement

    
    
    SELECT * FROM Sessions  
      
  
Atlas SQL returns all documents from the `Sessions` collection.

### LIMIT Statement

    
    
    SELECT * FROM Users LIMIT 2  
      
  
Atlas SQL returns two documents from the `Users` collection.

### WHERE Statement

    
    
    SELECT * FROM Users WHERE name='Jon Snow'  
      
  
Atlas SQL returns documents from the `Users` collection where the user's
`name` is `Jon Snow`.

For an Atlas SQL command reference, see SQL Reference.

← Query with SQLConnect →

