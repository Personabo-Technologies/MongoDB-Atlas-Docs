Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Online Archives

Share Feedback

On this page

  * View Online Archives
  * Retrieve an Online Archive Using the Atlas CLI
  * Retrieve an Online Archive Using the API
  * Retrieve All Online Archives for a Cluster Using the API
  * View Online Archives in the UI
  * Edit an Archiving Rule
  * Edit an Archiving Rule Through the Atlas CLI
  * Edit an Archiving Rule Through the API
  * Edit an Archiving Rule Through the UI
  * Edit the Partition on the Cloud Object Store
  * Query Online Archive
  * Connection String
  * Performance Considerations
  * Query Price
  * Delete an Online Archive
  * Delete an Online Archive Through the Atlas CLI
  * Delete an Online Archive from the UI
  * Delete an Online Archive Through the API

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

After you configure an online archive, you can do the following:

  * View your online archive

  * Edit your online archive

  * Query your online archive

  * Delete your online archive

## View Online Archives

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

You can view the list of online archives for a cluster through the Atlas CLI,
Atlas UI, and API.

### Retrieve an Online Archive Using the Atlas CLI

To list all online archive for a cluster using the Atlas CLI, run the
following command:

    
    
    atlas clusters onlineArchives list [options]  
      
  
To return the details for the online archive you specify using the Atlas CLI,
run the following command:

    
    
    atlas clusters onlineArchives describe <archiveId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas clusters onlineArchives list and atlas
clusters onlineArchives describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Retrieve an Online Archive Using the API

To retrieve an online archive through the API, send a `GET` request to the
onlineArchives endpoint with the unique ID of the online archive to retrieve.
To learn more about the API syntax and options, see API.

### Retrieve All Online Archives for a Cluster Using the API

To retrieve all the online archives configured for a cluster using the API,
send a `GET` request to the onlineArchives endpoint for the cluster. To learn
more about the syntax and options, see API.

### View Online Archives in the UI

To view the list of Online Archives:

1

#### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

#### Navigate to the Online Archive tab for your cluster.

  1. Click the name of the cluster.

  2. Click the Online Archive tab to view the list of online archives, if any, for the cluster.

The page displays the online archives for the cluster. For each online
archive, you can see the following information:

Column Name

|

Description  
  
|  
  
Archive Field

|

The date field based on which documents are archived.  
  
Archive Last Updated

|

The date when the archive was last modified.  
  
Archival Age Limit

|

The number of days used to qualify documents for archiving.  
  
Deletion Age Limit

|

The number of days after which to delete the data in the archive.  
  
Partition Fields

|

The other commonly used query fields used for partitioning data on the cloud
object storage.  
  
Status

|

The status of the Online Archive. Value can be one of the following:

|

|  
  
|  
  
Pending

|

Indicates documents are queued for archive, but archiving has not yet started.  
  
Archiving

|

Indicates archiving has started. In this state, the documents that meet the
criteria for archiving are being archived.  
  
Idle

|

Indicates online archive is waiting for the next archival job to start.  
  
Pausing

|

Indicates that you have requested to pause archiving. In this state, Atlas is
finishing the running archiving operation and therefore, Atlas has not yet put
archiving on hold. The online archive transitions to the `Paused` state when
the running archiving operation finishes.  
  
Paused

|

Indicates archiving has been temporarily stopped. In this state, previously
archived documents continue to be available on the cloud object storage for
querying, but the specified archiving operation on the active cluster is put
on hold and additional documents are not archived. You can resume archiving
for paused archives at any time.  
  
Orphaned

|

Indicates collection associated with an active or paused online archive was
deleted. Atlas will not automatically delete the archived data. You must
manually delete the online archives associated with the deleted collection.  
  
Deleted

|

Indicates online archive was deleted. When you delete an online archive,
associated archived documents are removed from the cloud object storage.  
  
Actions

|

Operations that you can perform on the Online Archive.  
  
## Edit an Archiving Rule

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

You can modify the number of days to keep data on the Atlas cluster (the Age
Limit) or the custom JSON query used to select documents for archiving from
the Atlas UI and API. You can't change the archiving criteria from Date Match
to Custom Filter, or vice versa.

### Edit an Archiving Rule Through the Atlas CLI

To update an online archive for a cluster using the Atlas CLI, run the
following command:

    
    
    atlas clusters onlineArchives update <archiveId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters onlineArchives update.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Edit an Archiving Rule Through the API

To edit an online archive through the API, send a `PATCH` request to the
onlineArchives endpoint with the unique ID of the online archive to update. To
learn more about the API syntax and options, see API.

### Edit an Archiving Rule Through the UI

To edit an online archive, in your Atlas UI:

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

#### Click the ellipsis (`...`) in the Actions column for the online archive
to display the list of allowed actions.

You can:

  * Pause Archiving (only if state is Active)

  * Edit Archive

  * Delete Archive

  * Resume Archiving (only if state is Paused)

4

#### Select Edit Archive from the dropdown to make changes to your archiving
rule, the number of days to keep archived data, and the time window for
running data archiving jobs.

You can change the archiving criteria and the number of days after which to
delete archived data.

  * To edit Date Match criteria, modify the number of days Atlas stores data on the active Atlas cluster in the Archival Age Limit section.

  * To edit Custom Criteria, enter a valid JSON filter to select the documents for archiving.

## Note

Atlas uses the specified query with the db.collection.find(query) command.
Custom queries do not support JavaScript expressions. Also, you can't pass an
empty document `{}` to return all documents.

  * To modify the number of days after which Atlas deletes archived data, enter or modify the number of days in the Deletion Age Limit section. You can specify between `7` and `9125` days, or leave the field empty to disable the data expiration rule. It takes 24 hours for this change to take effect.

## Note

Atlas Online Archive data expiration is available as a Preview feature. The
feature and the corresponding documentation may change at any time during the
Preview stage.

  * To modify the scheduled time for data archiving jobs, make changes to any of the following:

    * Frequency. You can choose to run the job every day, on a specific day of the week, or on a specific date every month. If you wish to archive on the 29th, 30th, or 31st of every month, Atlas doesn't run the archiving job for those months that don't include those dates.

    * Time window. Select the period of time during which you want Atlas to run the data archiving job. You must specify a minimum of two hours.

You can also disable the schedule by toggling Schedule Archive Window. If you
disable the schedule, Atlas reverts to the default schedule and runs the
archiving job periodically.

Atlas starts using the new data archiving schedule immediately after you
change it. However, if an archiving job is currently running, Atlas doesn't
interrupt the running job and the setting takes effect after the job
completes.

5

#### Click Save for the changes to take effect.

## Note

It takes 24 hours for changes to Deletion Age Limit to take effect.

### Edit the Partition on the Cloud Object Store

You can't modify the partition fields or structure from the Atlas UI or API.
However, you can manually migrate the data from the cloud object storage using
`mongodump`, delete the online archive, use `mongorestore` to restore the data
on the Atlas cluster, and then create a new online archive for the collection
with the desired partition fields and structure.

## Query Online Archive

You can run queries against your archived data.

### Connection String

To run queries, you must first connect to your Online Archive. Your cluster
connection string allows you to only query data in your Atlas cluster. To
query your Online Archive, you must use one of the following:

  * Connect to Online Archive and Cluster \- this read-only connection string allows you to read data directly from the live cluster. This impacts available resources for IOPS, and from your Online Archive.

  * Connect to Online Archive \- this read-only connection string allows you to read data from the Online Archive only and doesn't affect cluster resources.

### Performance Considerations

In general, your queries against archived data are much slower than your
queries against data on the Atlas cluster. When you query data in your cluster
and Online Archive through the federated connection string:

  * Blocking queries, such as sorts that consume and process all input documents to the sort operation before returning results, have performance characteristics associated with the slowest storage, the archive, being queried. The sort operations require all data from the sources being queried before returning the results.

  * Streaming queries, such as finds, have performance characteristics associated with the highest performing storage, the Atlas cluster, being queried. Atlas returns the results as soon as they are available, which means returning results from the archive takes longer than returning results from the Atlas cluster.

### Query Price

For your federated and archive-only queries, you incur costs for the following
items.

#### Data Scan

During data scan, Atlas processes data from both the cluster and the archive.
Atlas runs as much of the query on the cluster as it can to minimize the
amount of data it needs to scan. For example, for a `match` query that
specifies a specific value, Atlas only retrieves documents with the specified
value from the cluster. Atlas then combines the retrieved documents with the
archived data and returns.

For blocking queries that need to access all data stored in the underlying
cluster, Atlas retrieves all data. For example, for a `sort` (with no
`match`), Atlas retrieves all data from the cluster and archive to be sorted.

#### Data Access

MongoDB charges a fee for each partition that you query in the archive. If
your query requires querying specific partitions, MongoDB downloads the
partitions and each downloaded partition corresponds to a single access.

#### Data Seek

To find partitions based on the query and query fields, Atlas runs operations
on the archive. Each such operation that Atlas runs finds up to 1000
partitions. Atlas runs the minimum number of required operations to find the
partitions required to satisfy the query. For example, if your query requires
100 partitions that are covered in your query fields, Atlas runs only one
operation to satisfy the query.

#### Data Transfer

Data that is transferred to the federated infrastructure incurs data transfer
costs.

## Delete an Online Archive

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

You can delete an online archive through the Atlas UI and API. When you remove
an online archive, Atlas deletes all the files and metadata on the online
archive storage after a period of five days. After you delete this data, you
can't restore it.

If you drop a database or collection configured for online archive, the data
from the collection, if archived, continues to be available on the cloud
object storage. You incur costs for storage on the cloud object storage.
Alternatively, if you delete the cluster, Atlas deletes all the online
archives configured for the cluster. This also deletes any archived data from
the cloud object storage.

If you delete all the online archives, you also delete the federated database
instance and you create a new federated database instance when you create an
online archive again.

After you delete an online archive, its state moves to `Deleted`. You can
create another online archive for the same database, collection, and fields as
the deleted online archive if there is no other online archive for the same
database, collection, and fields in the `Active` state.

### Delete an Online Archive Through the Atlas CLI

To delete an online archive for a cluster using the Atlas CLI, run the
following command:

    
    
    atlas clusters onlineArchives delete <archiveId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters onlineArchives delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Delete an Online Archive from the UI

To delete an online archive, in your Atlas UI:

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

#### Click the ellipsis (`...`) in the Actions column for the online archive
to display the list of allowed actions.

You can:

  * Pause Archiving (only if state is Active)

  * Edit Archive

  * Delete Archive

  * Resume Archiving (only if state is Paused)

4

#### Select Delete Archive from the ellipsis menu to display the Delete Online
Archive confirmation window.

5

#### Enter the name of the online archive to delete and click Delete.

### Delete an Online Archive Through the API

To delete an online archive through the API, send a `DELETE` request to the
onlineArchives endpoint with the unique ID of the online archive to delete. To
learn more about the syntax and options, see API.

← Connect to Your Online ArchiveManage Private Endpoints for Online Archives →

