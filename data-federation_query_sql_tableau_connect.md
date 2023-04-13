Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect from Tableau

Share Feedback

On this page

  * Prerequisites
  * Procedure

This page describes how to connect to Atlas Data Federation with Tableau using
the Tableau Named Connector.

## Prerequisites

  * A federated database instance that is mapped to one or more data stores.

## Note

If some or all of your data comes from an Atlas cluster, you must use MongoDB
version 5.0 or greater for that cluster to take advantage of Atlas SQL.

  * Tableau Desktop or Server.

## Procedure

The following procedure guides you through installing the necessary tools,
finding your federated database instance connection information, and
connecting to your federated database instance with Tableau.

### Download the JDBC Driver and Tableau Connector

1

#### Download the MongoDB JDBC Driver.

  1. Download the latest MongoDB JDBC Driver version. Select the `all.jar` file, which includes necessary driver classes and dependencies.

  2. Move the downloaded `.jar` file into the appropriate directory for your operating system:

Operating System

|

Folder Path  
  
|  
  
Windows

|

`C:\Program Files\Tableau\Drivers`  
  
MacOS

|

`~/Library/Tableau/Drivers`  
  

2

#### Download and install the Tableau Named Connector.

  1. Download the Taco file.

  2. Move the downloaded Taco file into the appropriate directory for your operating system:

Operating System

|

Folder Path  
  
|  
  
Windows

|

`C:\Documents\My Tableau Repository\Connectors`  
  
MacOS

|

`~/Documents/My Tableau Repository/Connectors`  
  

## Important

### Updating Your Connector

If you download a new version of the Tableau Named Connector, delete the old
Tableau Named Connector file from your Connectors directory to ensure that
Tableau uses the latest version.

### Get Your federated database instance Connection Information

1

#### Navigate to your federated database instance.

In Atlas, select Data Federation from the left navigation panel.

2

#### Click Connect to open the federated database instance connection modal.

3

#### Select Connect using the Atlas SQL Interface.

4

#### Select Tableau Connector.

5

#### Copy your connection information.

Atlas Data Federation provides a connection string to connect to your
federated database instance. You'll need this in a later step.

### Connect with Tableau

1

#### Open Tableau Desktop or Tableau Server.

2

#### Navigate to the Connect menu.

3

#### Select MongoDB Atlas by MongoDB.

A connection modal displays.

4

#### Enter the connection information that you copied from Atlas Data
Federation.

Enter the following information:

|  
  
|  
  
MongoDB URI

|

Your connection string from step 5 of Get Your federated database instance
Connection Information.  
  
Database

|

Your virtual database name.  
  
Username

|

The MongoDB user to connect with.  
  
Password

|

The MongoDB user's password.  
  
## Tip

If you created your first virtual database during this tutorial, your
database's name is `Database0`. Otherwise, find your virtual database's name
in your Atlas SQL federated database instance interface under the Data
Federation tab.

5

#### Click Sign In.

← Connect from DBeaverConnect from the MongoDB Shell →

