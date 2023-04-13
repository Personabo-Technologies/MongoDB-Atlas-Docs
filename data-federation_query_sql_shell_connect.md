Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect from the MongoDB Shell

Share Feedback

On this page

  * Prerequisites
  * Procedure
  * Run SQL Queries

This page describes how to connect to a federated database instance through
the MongoDB Shell (`mongosh`).

## Prerequisites

  * A federated database instance that is mapped to one or more data stores.

## Note

If some or all of your data comes from an Atlas cluster, you must use MongoDB
version 5.0 or greater for that cluster to take advantage of Atlas SQL.

## Procedure

1

### Navigate to your federated database instance.

If it isn't already displayed, select Data Federation from the left navigation
panel.

2

### Click Connect to open the federated database instance connection modal.

3

### Select Connect with the MongoDB Shell.

4

### Install the MongoDB Shell if you haven't already.

If you do not have the MongoDB Shell installed:

1

#### Select I do not have the MongoDB Shell installed inside the connection
modal.

2

#### Select your operating system from the modal dropdown menu.

3

#### Follow the installation instructions for your operating system provided
in the modal.

4

####  _(Optional)_ Confirm that your `mongosh` installation was successful.

To check that your installation was successful, in your terminal, run:

    
    
    mongosh --version  
      
  
If the installation was successful, `mongosh` displays a version.

If you already have the MongoDB Shell installed:

1

#### Select I have the MongoDB Shell installed inside the connection modal.

2

#### Select `mongosh` from the modal dropdown menu.

## Note

The MongoDB Shell, or `mongosh`, is separate from the `mongo` versions in the
modal dropdown menu.

If you want to ensure that you have `mongosh` installed, in your terminal,
run:

    
    
    mongosh --version  
      
  
If `mongosh` is installed, it displays a version.

5

### Select your authentication method.

Your authentication method depends on how your Database Access is configured.
To learn more about database access, see Configure Database Users.

You can choose:

  * Password (SCRAM), or

  * X.509.

Atlas Data Federation provides a connection string for your authentication
method.

6

### Copy and run your connection string.

If you selected the Password (SCRAM) authentication method, you are prompted
for a password for the connecting user.

7

###  _(Optional)_ Confirm the connection to your federated database instance.

To confirm that you are connected to your federated database instance, using
`mongosh`, run:

    
    
    show dbs  
      
  
If you successfully connected to your federated database instance that is
mapped to a data store, `mongosh` displays the names of your virtual
databases.

## Run SQL Queries

You can run Atlas SQL queries against your federated database instance virtual
collections using the MongoDB Shell.

For an Atlas SQL command reference, see SQL Reference.

### Syntax

Atlas SQL supports an aggregation pipeline stage syntax and a short-form
syntax for constructing the SQL queries. You can use either of these syntaxes
to write queries in the MongoDB Shell:

#### Aggregation Pipeline Stage Syntax

You can use the `$sql` aggregation pipeline stage to write Atlas SQL queries.
See `$sql` for a list of properties you must provide to `$sql`.

## Note

Atlas SQL uses the dialect `mongosql`.

The following example uses `$sql` syntax to execute the Atlas SQL statement
`select * from Users limit 2`:

    
    
    db.aggregate( [ { $sql: { statement: "select * from Users limit 2", format: "jdbc", dialect: "mongosql" } } ] )  
      
  
#### Short-form Syntax

You can use a short-form syntax, `db.sql`, to supply an Atlas SQL statement
directly.

## Important

Short-form syntax is not stable and may change in the future.

    
    
    db.sql( "select * from Users limit 2" )  
      
  
### Examples

Try running the following Atlas SQL queries against the Get Started sample
federated database instance, or modify them to read your own data.

## Note

These examples use short-form syntax.

#### SELECT Statement

    
    
    db.sql("select * from Sessions")  
      
  
Atlas SQL returns all documents from the `Sessions` collection.

#### LIMIT Statement

    
    
    db.sql("select * from Users limit 2")  
      
  
Atlas SQL returns two documents from the `Users` collection.

#### WHERE Statement

    
    
    db.sql("select * from Users where name='Jon Snow'")  
      
  
Atlas SQL returns documents from the `Users` collection where the user's
`name` is `Jon Snow`.

← Connect from TableauSchema Management →

