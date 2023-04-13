Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Online Archive

Share Feedback

On this page

  * Overview
  * Configure Online Archive Through the Atlas CLI
  * Configure Online Archive Through the API
  * Configure Online Archive Through the User Interface
  * Limitations

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

## Overview

You can configure data in a collection to be archived by specifying an
archiving rule. The archiving rule for a:

  * Time series collection is a combination of a time that is used to determine when to archive data and a numeric value representing the number of days that the Atlas cluster stores the data.

  * Standard collection can be one of the following:

    * A combination of a date that is used to determine when to archive data and a numeric value representing the number of days that the Atlas cluster stores the data.

    * A custom query that is used to select the documents to archive.

To configure your Atlas cluster for online archive:

  1. Create an archiving rule by providing the collection namespace and the criteria for selecting data to archive in the collection.

  2. (Optional) Specify commonly queried fields to partition archived data.

## Configure Online Archive Through the Atlas CLI

To create an online archive for a cluster using the Atlas CLI, run the
following command:

    
    
    atlas clusters onlineArchives create [options]  
      
  
To watch for a specific online archive to become available using the Atlas
CLI, run the following command:

    
    
    atlas clusters onlineArchives watch <archiveId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas clusters onlineArchives create and atlas
clusters onlineArchives watch.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Configure Online Archive Through the API

To configure an online archive from the API, send a `POST` request to the
onlineArchives endpoint. If the cluster already has an `Active` online archive
with the same archiving rule for the same database and collection, the
operation will fail. However, if the existing online archive is in `Paused` or
`Deleted` state, the new online archive is created and its status is set to
`Active`. To learn more about the syntax and options, see API.

## Configure Online Archive Through the User Interface

To configure an Online Archive, in your Atlas UI:

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Navigate to the Online Archive tab for your cluster.

  1. Click the name of the cluster.

  2. Click the Online Archive tab to view the list of online archives, if any, for the cluster.

3

### Start configuring online archive for your collection.

To configure an online archive for your collection, click:

  * Configure Online Archive button the first time.

  * Add Archive button subsequently.

4

### Review the Online Archive Overview and click Next to proceed.

5

### Create an Archiving Rule by providing the following information.

  1. Specify the collection namespace, which includes the database name, the dot (`.`) separator, and the collection name (that is, `<database>.<collection>`), in the Namespace field.

You can't modify the namespace once the online archive is created.

  2. Specify the criteria for selecting documents to archive for the type of collection you want to archive.

Standard Collection

Time-Series Collection

For a standard collection, specify the criteria for selecting documents to
archive under the Date Match or Custom Criteria tab in the Atlas User
Interface.

Date Match

Custom Criteria

To select documents from the collection using a combination of a date field
and number of days:

    * Specify an already indexed date field from the documents in the collection. To specify a nested field, use the dot notation.

    * Specify the number of days to keep the data in the Atlas cluster.

    * Choose the date format of the specified date field.

If you choose any of the following formats, the value of specified date field
must be the BSON type `long`:

      * `EPOCH_SECONDS`

      * `EPOCH_MILLIS`

      * `EPOCH_NANOSECONDS`

## Important

You can't modify the date field once the online archive is created.

## Note

Atlas runs an index sufficiency query to determine the efficiency of the
archival process. If the number of documents scanned to the number of
documents returned is 10 or more, the query result triggers an `Index
Sufficiency Warning`. This warning indicates that you have insufficient
indexes for an efficient archival process. For date-based archives, you must
index the date field. For custom criteria that use an expression, Atlas might
first convert a value before it evaluates it against the query.

6

### Optional: Specify how many days you want to store data in the online
archive and a time window when you want Atlas to run the archiving job.

  1. (Optional) Expand Advanced Settings to specify Deletion Age Limit.

## Note

Atlas Online Archive data expiration is available as a Preview feature. The
feature and the corresponding documentation may change at any time during the
Preview stage.

By default, Atlas doesn't delete archived data. However, if you toggle the
Deletion Age Limit to enable deletion, you can specify between `7` to `9125`
days (25 years) to keep archived data. Atlas deletes archived data after the
number of days you specify here. This data expiration rule takes effect `24`
hours after you set the Deletion Age Limit.

## Warning

Once Atlas deletes the data, you can't recover the data.

  2. (Optional) Expand Advanced Settings to Schedule Archiving Window.

By default, Atlas periodically runs a query to archive data. However, you can
toggle the Schedule Archiving Window to explicitly schedule the time window
during which you want Atlas to archive data. You can specify the following:

    * Frequency. You can choose to run the job every day, on a specific day of the week, or on a specific date every month. If you wish to schedule the data archiving job on the 29th, 30th, or 31st of every month, Atlas doesn't run the archiving job for those months that don't include those dates (for example, February).

    * Time window. Select the period of time during which you want Atlas to run the data archiving job. You must specify a minimum of two hours. If a running job doesn't complete during the specified time window, Atlas continues to run the job until it completes.

7

### Click Next to specify the most commonly queried fields.

8

### Specify the two most frequently queried fields in your collection to
create partitions in your online archive.

## Note

Archive must have at least one partition field.

Standard Collection

Time-Series Collection

Date Match

Custom Criteria

Enter up to two most commonly queried fields from the collection in the Second
most commonly queried field and Third most commonly queried field fields
respectively. To specify nested fields, use the dot notation. Do not include
quotes (`""`) around nested fields that you specify using dot notation.

## Warning

You can't specify field names that contain periods (`.`) for partitioning.

The specified fields are used to partition your archived data. Partitions are
similar to folders. The date field is in the first position of the partition
by default for the Date Match criteria. You can move another field to the
first position of the partition if you frequently query by that field.

The order of fields listed in the path is important in the same way as it is
in Compound Indexes. Data in the specified path is partitioned first by the
value of the first field, and then by the value of the next field, and so on.
Atlas supports queries on the specified fields using the partitions.

For example, suppose you are configuring the online archive for the `movies`
collection in the `sample_mflix` database. If your archived field is the
`released` date field, which you moved to the third position, your first
queried field is `title`, and your second queried field is `plot`, your
partition will look similar to the following:

    
    
    /title/plot/released  
      
  
Atlas creates partitions first for the `title` field, followed by the `plot`
field, and then the `released` field. Atlas uses the partitions for queries on
the following fields:

  * the `title` field,

  * the `title` field and the `plot` field,

  * the `title` field and the `plot` field and the `released` field.

Atlas can also use the partitions to support a query on the `title` and
`released` fields. However, in this case, Atlas would not be as efficient in
supporting the query as it would be if the query were on the `title` and
`plot` fields only. Partitions are parsed in order; if a query omits a
particular partition, Atlas is less efficient in making use of any partitions
that follow that. Since a query on `title` and `released` omits `plot`, Atlas
uses the `title` partition more efficiently than the `released` partition to
support this query.

Atlas can't use the partitions to support queries on fields not specified
here. Also, Atlas can't use the partitions to support queries that include the
following fields without the `title` field:

  * the `plot` field,

  * the `released` field, or

  * the `plot` and `released` fields.

The value of a partition field can be up to a maximum of 700 characters.
Documents with values exceeding 700 characters are not archived.

  * Choose fields that contain only characters supported on AWS. To learn more about the characters to avoid, see Creating object key names. Atlas skips and doesn't archive documents that contain unsupported characters.

  * Choose fields that do not contain polymorphic data. Atlas determines the data type of a partition field by sampling 10 documents from the collection. Atlas will not archive a document if the specified field value in a document does not match values in other documents in the same collection.

  * Choose query fields that do not have high cardinality unless you always use those fields in your queries. Query fields, such as `_id`, with possibly unique and large number of values can cause operations such as `count` to open all partitions resulting in high latency.

  * Choose fields that you query frequently and order them from the most frequently queried in the first position to the least queried field in the last position. For example, if you frequently query on the date field, then leave the date field in the first position. But if you frequently query on another field, then that field should be in the first position.

## Note

For fields of type `string` with high cardinality, Atlas creates a large
number of partitions. MongoDB doesn't recommend `string` type fields with high
cardinality as a query field.

Atlas supports the following partition attribute types:

  * `date`

  * `int`

  * `long`

  * `objectId`

  * `string`

  * `uuid`

## Note

Partition fields of type UUID must be of binary subtype 4. Atlas skips
partition fields of type UUID with subtype 3.

To learn more about the supported partition attribute types, see Partition
Attribute Types.

While partitions improve query performance, queries that don't contain these
fields require a full collection scan of all archived documents, which will
take longer and increase your costs. To learn more about how partitions
improve your query performance in Atlas Data Federation, see Data Structure in
S3.

9

### Click Next to review and confirm the online archive settings.

You can review the following archiving rule settings:

  * The name of the database and collection

  * The name of the date field (for Date Match only)

  * The number of days to keep data on the Atlas cluster (for Date Match only)

  * The number of days after which to delete archived data

  * The frequency and time window for archiving data

  * The custom query to use to identify data to archive (for Custom Criteria only)

  * The partition fields

Click Back to edit these settings if needed.

10

### Copy and run the displayed query in your `mongosh` shell to see the
documents that match the criteria in the rule you defined in step 5.

You can run explain on the query to check whether it uses an index. Proceed to
the next step to create the index if the fields are not indexed. If the fields
are already indexed, skip to step 11.

11

### (Optional) Copy and run the displayed query in your `mongosh` to create
the required index. This ensures that your data is indexed for optimal
performance.

12

### Verify and confirm your archiving rule.

  1. Click Begin Archiving in the Confirm an online archive tab.

  2. Click Confirm in the Begin Archiving window.

## Note

Once your document is queued for archiving, you can no longer edit the
document. See Restore Archived Data to move archived data back into the live
Atlas cluster.

## Limitations

You can create up to 50 online archives per cluster and up to 20 can be active
per cluster. The following limitations apply:

  * You can configure multiple online archives in the same namespace, but only one can be active at any given time.

  * You can't create multiple online archives on the same fields in the same collection.

  * You can't access your online archive during the following scenarios:

    * A full outage of the primary region of your cluster.

    * An outage of AWS S3 where your archived data is stored.

  * You can't use an archiving rule for more than one collection.

## Note

If your goal is to archive data from several collections, you must create an
archiving rule for each collection.

← Archive DataSet Up a Private Endpoint for Online Archives →

