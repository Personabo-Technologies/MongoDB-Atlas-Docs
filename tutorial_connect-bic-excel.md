Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect from Excel

Share Feedback

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

For M10+ clusters that have enabled the BI Connector for Atlas, the Connect
dialog provides the details to connect via the BI Connector for Atlas.

## Prerequisites

Windows

macOS

  * Atlas cluster with BI Connector for Atlas enabled

  * Create a system Data Source Name (DSN)

## Connect from Microsoft Excel

Windows

macOS

1

### Start Microsoft Excel.

Start Microsoft Excel and open a blank worksheet.

2

### Use the Data Connection Wizard to set up the connection.

click to enlarge

  1. Click the Data tab.

  2. Select From Other Sources >

From Data Connection Wizard option.

  3. Select ODBC DSN from the list of data source options and click Next.

  4. Select the DSN created for your Atlas cluster and click Next.

  5. Select a database and collection from which to import data and click Next.

  6. Save the data connection file and click Finish.

If you wish to re-use this connection in the future, you can select it from
the Data > Get External Data > Existing Connections menu.

  7. In the final wizard window,specify a format for your worksheet. Click OK when finished.

## Additional Reference

For more information on the MongoDB Connector for Business Intelligence, see
MongoDB Connector for BI Manual.

← Create a System DSNConnect from Tableau Desktop →

