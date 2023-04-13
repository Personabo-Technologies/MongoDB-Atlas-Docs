Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect from DBeaver

Share Feedback

On this page

  * Prerequisites
  * Procedure
  * Run SQL Queries

This page describes how to connect to your federated database instance with
DBeaver.

## Prerequisites

  * A federated database instance mapped to one or more data stores.

## Note

If some or all of your data comes from an Atlas cluster, you must use MongoDB
version 5.0 or greater for that cluster to take advantage of Atlas SQL.

  * DBeaver (Community Edition).

  * The MongoDB JDBC Driver.

## Procedure

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

A new SQL console window that is connected to the virtual database you
selected opens.

3

### Enter a SQL query in the console.

4

### Click Execute SQL Statement to run your SQL query.

If the query is successful, the results are displayed in a table view below
your query.

Try running the following Atlas SQL queries against the Get Started sample
federated database instance, or modify them to read your own data.

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

← Connect from JDBC DriverConnect from Tableau →

