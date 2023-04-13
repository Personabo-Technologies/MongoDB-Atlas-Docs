Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Data Federation Costs

Share Feedback

You incur Atlas Data Federation costs for the following items:

  * Data processed by federated database instances

  * Data returned by federated database instances

## Total Data Processed

Atlas charges for the total number of bytes that Atlas Data Federation
processes from your underlying sources, rounded up to the nearest megabyte.
Atlas charges $5.00 per TB of processed data, with a 10 MB minimum processed
data per query.

You incur "Data Processed" costs for the amount of data that Atlas Data
Federation processes to return results for your queries in addition to the
"Data Returned" cost for the amount of data that Atlas Data Federation
returns. For example, for a 10 GB file, you incur the following "Data
Processed" cost in addition to the "Data Returned" cost:

  * If you have no partitions or if Atlas Data Federation needs to read the entire file to return results for the query, you incur 10 GB of "Data Processed" cost.

  * If you have 10 partitions of 1 GB each, Atlas Data Federation targets and reads a single partition. Therefore, you incur 1 GB of "Data Processed" cost.

You can use partitioning strategies and compression in AWS S3 to reduce the
amount of processed data. You can also configure query limits to limit the
amount of data that Atlas Data Federation processes for your federated
database instances and control costs.

## Total Data Returned and Transferred

Atlas charges for the total number of bytes returned and transferred by your
federated database instance. This total is the sum of all the following data
transfers:

  * The number of bytes returned to the client while reading query results

  * The number of bytes transferred between Data Federation query nodes while executing a query

  * The number of bytes written by Data Federation during `$out` or `$merge` operations

The cost of data transfer depends on the Cloud Service Provider charges for
same-region, region-to-region, or region-to-internet data transfer. AWS
charges $0.01 per GB for the number of bytes returned and transferred within
the same AWS region and for the number of bytes returned to the client.

## Tip

### See also:

  * Atlas pricing page

  * Set Up and Query Data Federation

← Serverless Instance CostsData Transfer →

