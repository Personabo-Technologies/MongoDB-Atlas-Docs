Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Download Query Logs

Share Feedback

On this page

  * Required Permissions
  * Download Query Logs from the UI
  * Download Query Logs Through the API

You can download logs of your {fdi+} queries from the Atlas user interface.
You can view the logs to determine information such as:

  * The number and type of executed queries.

  * The number of scanned documents.

The log is in JSON format and available as a `.gz` file. Atlas Data Federation
retains the logs for up to 30 days. By default, the logs are generated in UTC
format. You can modify the time zone in the User Preferences page to generate
and download the logs in your time zone. You can generate logs for:

  * The last four, eight, twelve, or twenty-four hours.

  * A specific date and time period.

## Required Permissions

To download Atlas Data Federation query logs, you must have the `Project Data
Access Read Only` or higher role.

## Download Query Logs from the UI

To download query logs:

1

### Log in to MongoDB Atlas.

2

### Select the Data Federation option on the left-hand navigation.

3

### Click __for your federated database instance and select Download Logs from
the dropdown.

4

### Select the Time Period for which you want to download logs from the
dropdown.

Choose one of the following time periods:

  * Last 4 Hours

  * Last 8 Hours

  * Last 12 Hours

  * Last 24 Hours

  * Custom Date

5

### Click Download Logs and follow your browser prompts to download the file.

The downloaded log filename is in the following format:

    
    
    <federated-database-instance-name>_<start-date>_<end-date>_queries.log.gz  
      
  
## Download Query Logs Through the API

To download query logs using the API, send a `GET` request to the Data
Federation `queryLogs.gz` endpoint. To learn more about the API syntax and
options, see Download Query Logs for One Federated Database.

← Retrieve Federated Database Instance Query HistoryQuery a Federated Database
Instance →

