Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# View and Download MongoDB Logs

Share Feedback

On this page

  * Procedure
  * Database Access Logs

Each `mongod`, `mongos`, and mongosqld tier keeps an account of its activity
in its own log file. Atlas retains the last 30 days of log messages and system
event audit messages for each tier in a cluster. The Performance Advisor
retains at most 7 days of logs for each process in a cluster.

## Important

You must have `Project Data Access Read Only` privileges or greater to
download logs.

## Note

`M0` free clusters and `M2/M5` shared clusters do not provide downloadable
logs.

## Procedure

Atlas CLI

Atlas UI

To download a zipped file containing the logs for the selected hostname using
the Atlas CLI, run the following command:

    
    
    atlas logs download <hostname> <mongodb.gz|mongos.gz|mongosqld.gz|mongodb-audit-log.gz|mongos-audit-log.gz> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas logs download.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

For information on reading MongoDB logs, refer to the Log Messages
documentation in the MongoDB manual.

## Database Access Logs

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

You can view authentication attempts that were made against your cluster. Both
successful and unsuccessful attempts are logged, including the timestamp of
the attempt and which user tried to authenticate.

← Integrate with PrometheusIntegrate Products and Services →

