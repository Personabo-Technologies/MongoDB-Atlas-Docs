Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Archive Data

Share Feedback

On this page

  * Overview
  * Cluster Requirements
  * Required Permissions
  * How Atlas Archives Data
  * Atlas Data Federation for Online Archive
  * Limitations
  * Viewing the Online Archive
  * Querying the Online Archive
  * Managing Query Limits for Online Archive
  * Editing Online Archives
  * Deleting Online Archives
  * Online Archive Costs
  * Manage Your Online Archive

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

## Overview

Atlas moves infrequently accessed data from your Atlas cluster to a MongoDB-
managed read-only Federated Database Instance on a cloud object storage. Once
Atlas archives the data, you have a unified view of your Atlas and Online
Archive data through a read-only federated database instance.

Atlas archives data based on the criteria you specify in an archiving rule.
The criteria varies based on the type of collection you want to archive:

Standard Collection

Time Series Collection

For standard collections, the criteria can be one of the following:

  * A combination of a date field to archive data and number of days to keep data on the Atlas cluster. When the current date exceeds the value of the specified date field, Atlas subtracts the number of days from the current time and then archives data after the time.

  * A custom query. Atlas runs the query specified in the archiving rule to select the documents to archive.

### Cluster Requirements

 _Online Archive_ in Atlas is available only on `M10` and greater clusters.

### Required Permissions

To create or delete an Online Archive, you must have one of these roles:

  * `Project Data Access Admin` role

  * `Project Cluster Manager` role

  * `Project Owner` role

### How Atlas Archives Data

To archive data:

  1. Atlas runs a query to determine the documents that match the criteria for archiving. Atlas refers to this query as a _job_.

By default, Atlas runs the job every five minutes. If the size or number of
documents to archive doesn't meet the threshold, Atlas expands the job
interval by five minutes, up to a maximum of four hours. If the job interval
reaches the maximum or if either the size or number of documents to archive
reaches the threshold, Atlas runs the job again and resets the job interval to
five minutes.

If you specify a time window when you want to run the job, Atlas runs the job
continuously during that time window. If a running job doesn't complete during
the time window, Atlas continues to run the job until it completes. If all
archiving jobs reach the maximum threshold for either the size or number of
documents to archive during three consecutive archive windows, we recommend
that you increase the frequency.

The threshold is 2GB per job.

Atlas runs an index sufficiency query to determine the efficiency of the
archival process. If the number of documents scanned to the number of
documents returned is 10 or more, the query result triggers an `Index
Sufficiency Warning`. This warning indicates that you have insufficient
indexes for an efficient archival process. For date-based archives, you must
index the date field. For custom criteria that use an expression, Atlas might
first convert a value before it evaluates it against the query.

  2. For documents that match the archival criteria, Atlas:

    1. Writes to up to a maximum of 10,000 partitions per data archiving job.

    2. Writes up to 2GB of document data to partitions on the cloud object storage for each unique combination of query field values except dates, which are grouped during each run to reduce the number of partitions.

    3. Writes each subsequent quantity of document data (up to 2 GB) with each query run.

Online Archive runs on your Atlas cluster and utilizes the same underlying
resources (e.g. IOPS). The default limit of 2GB per job prevents the operation
from utilizing too many resources. If your cluster is currently satisfying
workloads at the edge of its resource limits, you could push it past its
capacity by activating Online Archive. Ensure that your Atlas cluster has
excess resources before activating Online Archive.

If you activate Online Archive for an AWS cluster, the cloud object storage
exists in the same region in AWS as your cluster. If you activate Online
Archive for a Google Cloud or Azure cluster, Online Archive creates the
archive in the AWS region closest to your cluster's primary based on a
calculation of distance between the cluster and cloud object storage.

## Important

Atlas encrypts your archived data using Amazon's server-side encryption
S3-managed keys (SSE-S3) for archived data. It can't use any encryption-at-
rest encryption keys you might have used on your cluster data.

When you archive data, Atlas first copies the data to the cloud object storage
and then deletes the data from your Atlas cluster. WiredTiger does not release
the storage blocks of the deleted data back to the OS for performance reasons.
However, Atlas eventually automatically reuses these storage blocks for new
data. This helps the Atlas cluster to avoid fragmentation. To learn more about
reclaiming the disk space, see How do I reclaim disk space in WiredTiger?.

Atlas provides a unified endpoint. You can use it to query all databases and
collections on your live cluster and archived data using the same database and
collection name that you use in your Atlas cluster. You can't use the unified
endpoint over a Network Peering Connection, but you can set up a private
endpoint or use a standard internet connection over TLS.

## Atlas Data Federation for Online Archive

When you configure your `M10` or greater Atlas cluster for Online Archive,
Atlas creates a read-only Federated Database Instance, one per cluster, for
your archived data.

### Limitations

Online Archive doesn't support the following:

  * Writing to the Online Archive.

  * Configuring or administering the Online Archive federated database instance through the Atlas console, Atlas Data Federation CLI, or Atlas Data Federation API.

  * Archiving a capped collection.

  * GridFS.

### Viewing the Online Archive

To view your federated database instance for the Online Archive:

  1. Log in to the Atlas console.

  2. Click Data Federation from the left navigation in your Project page.

### Querying the Online Archive

To query your Online Archive data, use the connection string through the
Online Archive or federated database instance Connect button to connect to the
federated database instance.

You can also query your Online Archive data with SQL. To learn more, see Query
with SQL.

### Managing Query Limits for Online Archive

You can configure limits on the amount of data that is processed for your
queries against archived data to control the data processing costs for your
Online Archive. When the amount of processed data reaches any applicable
configured limit, Atlas won't execute any new queries and returns an error to
the client application that a limit has been reached. You can also optionally
configure query termination to terminate queries that exceed the limit. To
learn more about configuring query limits and query termination, see Manage
Atlas Data Federation Query Limits.

### Editing Online Archives

Once Atlas creates the Online Archive, you can't change the archiving criteria
from Date Match to Custom Filter, or vice versa.

### Deleting Online Archives

If you delete all the Online Archives, Atlas deletes the federated database
instances. After deleting all the Online Archives, if you create an Online
Archive with the same settings as a deleted Online Archive, Atlas creates a
new federated database instance for the new Online Archive.

## Online Archive Costs

Online Archive stores infrequently accessed data to lower the data storage
costs on your Atlas cluster. However, you incur costs for amount of data that
you transfer and query. To learn more about Online Archive costs, see the
Online Archive Costs.

## Manage Your Online Archive

You can configure an Online Archive for a collection on your cluster through
your Atlas console and API. Once you create an Online Archive, you can:

  * View the list of Online Archives.

  * Configure the connection method, standard or private endpoint, for your Online Archive

  * Edit an archiving rule.

  * Delete your Online Archive.

  * Pause archiving.

  * Restore archived data.

← Import Archive from S3Configure Online Archive →

