Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect from Qlik Sense

Share Feedback

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

For M10+ clusters that have enabled the BI Connector for Atlas, the Connect
dialog provides the details to connect via the BI Connector for Atlas.

## Prerequisites

  * Atlas cluster with BI Connector for Atlas enabled

  * Create a system Data Source Name (DSN)

  * Qlik Sense Desktop

## Procedure

1

### Start Qlik Sense Desktop.

Start the Qlik Sense desktop application.

2

### Create a Data Connection to the BI Connector for Atlas.

  1. Click Create a New App.

  2. Enter a name for the app and Create. If created successfully, Open app.

  3. Click Add data from files and other sources.

  4. Select ODBC from the list of data sources.

  5. In the Create New Connection window, in the System DSN, select the DSN that you created earlier.

Leave the Username and Password fields blank as the application uses the
username and password specified in the DSN during the ODBC set up.

  6. Click Create.

For example:

## Additional Reference

For more information on the MongoDB Connector for Business Intelligence, see
MongoDB Connector for BI Manual.

← Connect from Tableau DesktopConnect from MySQL Workbench →

