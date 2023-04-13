Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Fix Query Issues

Share Feedback

On this page

  * Alert Conditions
  * Common Triggers
  * Fix the Immediate Problem
  * Implement a Long-Term Solution
  * Monitor Your Progress

`Query Targeting` alerts indicate inefficient queries.

## Alert Conditions

You can configure the following alert conditions in the project-level alert
settings page to trigger alerts.

`Query Targeting: Scanned Objects / Returned` occurs if the number of
documents examined to fulfill a query relative to the actual number of
returned documents meets or exceeds a user-defined threshold. The default is
1000, which means that a query must scan more than 1000 documents for each
document returned to trigger the alert.

`Query Targeting: Scanned / Returned` occurs if the number of index keys
examined to fulfill a query relative to the actual number of returned
documents meets or exceeds a user-defined threshold. This alert is not enabled
by default.

Ideally, the ratio of scanned documents to returned documents should be close
to 1. A high ratio negatively impacts query performance.

## Example

The following mongod log entry shows statistics generated from an inefficient
query:

    
    
    <Timestamp> COMMAND  <query>  
      
    planSummary: COLLSCAN keysExamined:0  
    docsExamined: 10000 cursorExhausted:1 numYields:234  
    nreturned:4  protocol:op_query 358ms  
  
This query scanned 10,000 documents and returned only 4 for a ratio of 2500,
which is highly inefficient. No index keys were examined, so MongoDB scanned
all documents in the collection, known as a collection scan.

## Common Triggers

The query targeting alert typically occurs when there is no index to support a
query or queries or when an existing index only partially supports a query or
queries.

## Note

The changestream cursors that the Atlas Search process (`mongot`) uses for
replication can contribute to the query targeting ratio and trigger query
targeting alerts if the ratio is high.

## Fix the Immediate Problem

Add one or more indexes to better serve the inefficient queries.

The Performance Advisor provides the easiest and quickest way to create an
index. The Performance Advisor monitors queries that MongoDB considers slow
and recommends indexes to improve performance. Atlas dynamically adjusts your
slow query threshold based on the execution time of operations across your
cluster.

Click Create Index on a slow query for instructions on how to create the
recommended index.

## Note

It is possible to receive a Query Targeting alert for an inefficient query
without receiving index suggestions from the Performance Advisor if the query
exceeds the slow query threshold and the ratio of scanned to returned
documents is greater than the threshold specified in the alert.

In addition, you can use the following resources to determine which query
generated the alert:

  * The Real-Time Performance Panel monitors and displays current network traffic and database operations on machines hosting MongoDB in your Atlas clusters.

  * The MongoDB logs maintain an account of activity, including queries, for each `mongod` instance in your Atlas clusters.

  * The cursor.explain() command for `mongosh` provides performance details for all queries.

  * The Data Profiler records operations that Atlas considers slow when compared to average execution time for all operations on your cluster.

## Note

Enabling the Database Profiler incurs a performance overhead.

## Implement a Long-Term Solution

Refer to the following for more information on query performance:

  * MongoDB Indexing Strategies

  * Query Optimization

  * Analyze Query Plan

## Monitor Your Progress

Atlas provides two methods to visualize query targeting:

  * Query Targeting metrics, which highlight high ratios of objects scanned to objects returned.

  * The Query Profiler, which describes specific inefficient queries executed on the cluster.

### Query Targeting Metrics

You can view historical metrics to help you visualize the query performance of
your cluster. To view Query Targeting metrics in the Atlas UI:

  1. Click Database in the top-left corner of Atlas.

  2. Click View Monitoring on the dashboard for the database deployment.

  3. On the Metrics page, click the Add Chart dropdown menu and select Query Targeting.

The Query Targeting chart displays the following metrics for queries executed
on the server:

Metric

|

Description  
  
|  
  
Scanned Objects / Returned

|

Indicates the average number of documents examined relative to the average
number of returned documents.  
  
Scanned / Returned

|

Indicates the number of index keys examined to fulfill a query relative to the
actual number of returned documents.  
  
## Note

The changestream cursors that the Atlas Search process (`mongot`) uses for
replication can contribute to the query targeting ratio and trigger query
targeting alerts if the ratio is high.

If either of these metrics exceed the user-defined threshold, Atlas generates
the corresponding `Query Targeting: Scanned Objects / Returned` or `Query
Targeting: Scanned / Returned` alert.

## Note

You can also view Query Targeting ratios of operations in real-time using the
Real-Time Performance Panel.

### Query Profiler

The Query Profiler contains several metrics you can use to pinpoint specific
inefficient queries. You can visualize up to the past 24 hours of query
operations. The Query Profiler can show the Examined : Returned Ratio (index
keys examined to documents returned) of logged queries, which might help you
identify the queries that triggered a `Query Targeting: Scanned / Returned`
alert. The chart shows the number of index keys examined to fulfill a query
relative to the actual number of returned documents.

## Note

The default `Query Targeting: Scanned Objects / Returned` alert ratio differs
slightly. The ratio of the average number of documents scanned to the average
number of documents returned during a sampling period triggers this alert.

Atlas might not log the individual operations that contribute to the Query
Targeting ratios.

To access the Query Profiler:

  1. Click Database in the top-left corner of Atlas.

  2. Click View Monitoring on the dashboard for the database deployment.

  3. Click the Profiler tab.

← Fix Storage IssuesFix Lost Primary →

