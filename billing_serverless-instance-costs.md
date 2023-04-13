Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Serverless Instance Costs

Share Feedback

On this page

  * Usage Cost Summary
  * Read Processing Unit Pricing
  * Payment Methods

Serverless instances offer pay-per-operation pricing, meaning that you only
pay for the Processing Units consumed by your database operations and storage
consumed by your data and indexes. You do not need to specify a cluster size
since serverless instances seamlessly scale to accommodate changes in workload
traffic.

Serverless instances may be more cost effective for applications with low or
intermittent traffic. To learn more about serverless instances and use cases,
see Choose a Database Deployment Type.

## Usage Cost Summary

Operation pricing varies between cloud providers and geographic regions. All
operations are billed _per day_.

Name

|

Description

|

Price  
  
||  
  
Read Processing Unit (`RPU`)

|

Read operations to the database.

You are charged one `RPU` for each document read (up to 4KB) or for each index
read (up to 256 bytes).

If a document exceeds 4KB or an index exceeds 256B, Atlas covers each excess
chunk of 4KB or 256B with an additional `RPU`.

|

The price for each million `RPU`s decreases based on volume of reads in a day.
Starting prices range from $0.09 to $0.22 per million `RPU`s. [1] See Read
Processing Unit Pricing for price tier details.  
  
Write Processing Unit (`WPU`)

|

Write operations to the database.

You are charged one `WPU` for each combined document and index written (up to
1KB). `WPU`s start at 0 each day.

If a document and index exceed 1KB, Atlas covers each excess chunk of 1KB with
an additional `WPU`.

|

Range from $0.90 to $2.20 per million `WPU`s. [1]  
  
Storage

|

Logical document and index storage. This value includes the number of bytes of
all uncompressed BSON documents stored in all collections, plus the bytes
stored in their associated indexes.

|

Range from $0.20 to $0.70 per `GB` per month.  
  
Continuous Backup

|

Point-in-Time backups triggered by write events.

|

Range from $0.20 to $0.60 per `GB` per month.  
  
Restore from Backup

|

The time required to restore your serverless instance.

## Important

Data transfer as part of the backup and restore process is charged separately.

|

Range from $2.50 to $6.00 per restore hour.  
  
Data Transfer

|

Data transfer to and from the database. [1]

## Tip

If your data transfer costs are a significant portion of your bill, see How to
Reduce Data Transfer Costs.

|

  * Regional: $0.01 per `GB` for _all_ cloud providers and regions.

  * Cross-Region: range from $0.02 to $0.20 per `GB`.

  * Public Internet: range from $0.09 to $0.20 per `GB`.

  
  
[1]|  _(1, 2, 3)_ `RPU` and `WPU` prices are presented _per million_ , but you
are only charged for the amount you use. For example, if `WPU`s cost $1.25 per
million in your region; using 500,000 would cost $0.63. The same is true for
data transfer: you're only charged for the amount you transfer.  
|  
  
### Read Processing Unit Pricing

The price for each million (MM) `RPU`s depends on volume of reads that day.
`RPU`s start at 0 each day. Prices are in cascading tiers:

Tier

|

Description

|

Price  
  
||  
  
0-50 MM `RPU`s

|

The first 50 million `RPU`s in a day.

|

$0.09 to $0.22/MM  
  
50-550 MM `RPU`s

|

The next 500 million `RPU`s in a day.

|

$0.05 to $0.11/MM  
  
550 MM-20.55 B `RPU`s

|

The next 20 billion `RPU`s in a day.

|

$0.01 to $0.03/MM  
  
20.55+ B `RPU`s

|

All subsequent `RPU`s in a day.

|

Free  
  
## Example

If your application uses 560 million `RPU`s in a day, in a region with prices
of $0.10/MM, $0.06/MM, and $0.02/MM by tier, Atlas charges you $35.20:

  * $0.10/MM for the first 50 million ($5.00).

  * $0.06/MM for the next 500 million ($30.00).

  * $0.02/MM for the last 10 million ($0.20).

If that usage is typical for a day, your application costs approximately $1056
per month ($35.20 per day x 30 days).

In another example, if your application uses 0.5 million `RPU`s in a day in
the same region, Atlas charges you $0.05:

  * $0.10/MM for the first 0.5 million ($0.05).

If that usage is typical for a day, your application costs approximately $1.50
per month ($0.05 per day x 30 days).

## Payment Methods

## Warning

An unexpected, significant increase in serverless instance usage could result
in an expensive invoice. Use billing alerts to monitor usage.

You can pay for serverless instances with:

  * A payment method added through the Atlas console,

  * an Atlas subscription, or

  * Atlas credits.

← Cluster Configuration CostsData Federation Costs →

