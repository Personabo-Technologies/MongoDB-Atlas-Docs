Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect from MySQL Workbench

Share Feedback

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

For M10+ clusters that have enabled the BI Connector for Atlas, the Connect
dialog provides the details to connect via the BI Connector for Atlas.

## Prerequisites

  * Atlas cluster with BI Connector for Atlas enabled

  * MySQL Workbench 6.3 or later

## Note

Versions of MySQL Workbench that are compatible with MySQL server version 5.7
are also compatible with the BI Connector for Atlas.

We recommend MySQL Workbench version 6.3 or later to guarantee compatibility.

## Procedure

The following tutorial outlines the steps to connect using MySQL Workbench
6.3. Atlas supports both the Community and Commercial Editions.

1

### Start MySQL Workbench.

Start the MySQL Workbench 6.3.

2

### Create a New MySQL Connection.

  1. From the Welcome page, click on the plus sign (`+`):

Alternatively, you can create a new connection from the Manage Connections ...
screen.

  2. Enter the name for your connection.

  3. Configure the parameters for the connection. In the Parameters section, update the following fields:

Field Name

|

Description  
  
|  
  
Hostname

|

Enter the Hostname specified in the Atlas connect dialog.  
  
Port

|

Enter the Port specified in the Atlas connect dialog.  
  
Username

|

Enter either the user specified in the Atlas connect dialog or a different
database user for the cluster.

The user is specified in the format:

    
        | <username>?source=<database-name>  
      
  
where the `<database-name>` is the authentication database for the user.  
  
Password

|

Store the password in the keychain.  
  
Default Schema

|

Optional. The name of a database in the cluster to connect.  
  
  4. Configure the SSL settings for the connection. In the SSL section, update the following field:

Field Name

|

Description  
  
|  
  
Use SSL

|

Select If available.  
  
  5. Configure the advanced settings for the connection. In the Advanced section, update the following field:

Field Name

|

Description  
  
|  
  
Enable Cleartext Authentication Plugin

|

Select.  
  

3

### Click the `Test Connection` to test the connection.

If the connection is successful, click OK and Close the Connection setup
screen and return to the Welcome page.

If the connection fails, check the settings, including the MongoDB database
user credentials and the IP access list.

4

### Connect.

From the Welcome page, double-click on the newly created connection to connect
and open the SQL Editor.

## Additional Reference

For more information on the MongoDB Connector for Business Intelligence, see
MongoDB Connector for BI Manual.

← Connect from Qlik SenseConnect from Power BI Desktop (Windows) →

