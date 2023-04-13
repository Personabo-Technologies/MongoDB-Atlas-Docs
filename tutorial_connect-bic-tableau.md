Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect from Tableau Desktop

Share Feedback

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

For M10+ clusters that have enabled the BI Connector for Atlas, the Connect
dialog provides the details to connect via the BI Connector for Atlas.

The MongoDB Connector for Business Intelligence for Atlas (BI Connector) is
only available for `M10` and larger clusters.

The BI Connector is a powerful tool which provides users SQL-based access to
their MongoDB databases. As a result, the BI Connector performs operations
which may be CPU and memory intensive. Given the limited hardware resources on
`M10` and `M20` cluster tiers, you may experience performance degradation of
the cluster when enabling the BI Connector. If this occurs, upgrade to an
`M30` or larger cluster or disable the BI Connector.

## Prerequisites

Windows

macOS

  * Atlas cluster with BI Connector for Atlas enabled

  * Create a system Data Source Name (DSN) that uses the MongoDB ODBC driver

  * Tableau version 10.3 or later

## Procedure

Windows

macOS

1

### Start Tableau Desktop.

2

### Connect to the BI Connector for Atlas.

Select the MongoDB BI Connector as your Data Source for your Tableau book.

  1. From the left-hand navigation, under To a server, click More ... and select Other Databases (ODBC).

  2. Select the DSN that you just created from the DSN list.

  3. Enter the following fields in the Connection Attributes pane:

Field

|

Action  
  
|  
  
Server

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

Enter the password corresponding to the entered User.  
  
For example:

  4. Click Sign In.

## Additional Reference

For more information on the MongoDB Connector for Business Intelligence, see
MongoDB Connector for BI Manual.

← Connect from ExcelConnect from Qlik Sense →

