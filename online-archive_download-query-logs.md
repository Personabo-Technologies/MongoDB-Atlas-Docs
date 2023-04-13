Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Download Query Logs

Share Feedback

On this page

  * Required Permissions
  * Procedure

You can download logs of your Online Archive queries from the Atlas user
interface. You can view the logs to determine information such as:

  * The number and type of executed queries.

  * The number of scanned documents.

The log is in JSON format and available as a `.gz` file. Atlas retains the
logs for up to 30 days. By default, the logs are generated in UTC format. You
can modify the time zone in the User Preferences page to generate and download
the logs in your time zone. You can generate logs for:

  * The last four, eight, twelve, or twenty-four hours.

  * A specific date and time period.

## Required Permissions

To download your Online Archive query logs, you must have `Project Data Access
Read Only` or higher role.

### Procedure

To download query logs:

1

#### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

#### Navigate to the Online Archive tab for your cluster.

  1. Click the name of the cluster.

  2. Click the Online Archive tab to view the list of online archives, if any, for the cluster.

3

#### Click __for the Online Archive for which you want to download query logs
and select Download Online Archive Query Logs from the dropdown.

4

#### Select the Source for which you want to download logs.

You can chose one of these:

  * Online Archive Only to download logs for queries against your Online Archive only

  * Cluster and Online Archive to download logs for queries against both the Atlas cluster and Online Archive

5

#### Select the Time Period for which you want to download logs from the
dropdown.

You can chose one of these:

  * Last 4 Hours

  * Last 8 Hours

  * Last 12 Hours

  * Last 24 Hours

  * Custom Date

6

#### Click Download Logs and follow your browser prompts to download the file.

The downloaded log filename varies based on the Source for which you are
downloading the logs:

Online Archive Only

Cluster and Online Archive

    
    
    <cluster-name>_archive_only_<start-date>_<end-date>_queries.log.gz  
      
  
← Restore Archived DataLegacy Backups (Deprecated) →

