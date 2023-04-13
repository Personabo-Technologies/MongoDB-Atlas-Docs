Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Monitor and Improve Slow Queries

Share Feedback

On this page

  * Common Reasons for Slow Queries
  * Configure the Slow Query Threshold
  * Index Considerations
  * Access Performance Advisor
  * Index Suggestions
  * Create Suggested Indexes

 _Only available on M10+ clusters and serverless instances_

The Performance Advisor monitors queries that MongoDB considers slow and
suggests new indexes to improve query performance. The threshold for slow
queries varies based on the average time of operations on your cluster to
provide recommendations pertinent to your workload.

Recommended indexes are accompanied by sample queries, grouped by query shape,
that were run against a collection that would benefit from the suggested
index. The Performance Advisor doesn't negatively affect the performance of
your Atlas clusters.

You can also monitor query performance with the Query Profiler. To learn more,
see Monitor Query Performance.

## Note

If the slow query log contains consecutive `$match` stages in the aggregation
pipeline, the two stages can coalesce into the first `$match` stage and result
in a single `$match` stage. As a result, the query shape in the Performance
Advisor might differ from the actual query you ran.

## Common Reasons for Slow Queries

If a query is slow, common reasons include:

  * The query is unsupported by your current indexes.

  * Some documents in your collection have large array fields that are costly to search and index.

  * One query retrieves information from multiple collections with $lookup.

## Configure the Slow Query Threshold

By default, Atlas dynamically adjusts your slow query threshold based on the
execution time of operations across your cluster. To opt out of this feature
and instead use a fixed slow query threshold of 100 milliseconds, you can
disable the Atlas-managed slow operation threshold with the Atlas CLI or the
Atlas Administration API.

## Note

Atlas clusters with Atlas Search enabled don't support the Atlas-managed slow
query operation threshold.

For `M0`, `M2`, `M5` clusters and serverless instances, Atlas disables the
Atlas-managed slow query operation threshold by default and you can't enable
it.

### Disable the Atlas-Managed Slow Operation Threshold

To disable the Atlas-managed slow operation threshold and use a fixed
threshold of 100 milliseconds:

Atlas CLI

Atlas Administration API

To disable the Atlas-managed slow operation threshold for your project using
the Atlas CLI, run the following command:

    
    
    atlas performanceAdvisor slowOperationThreshold disable [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas performanceAdvisor slowOperationThreshold disable.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Enable the Atlas-Managed Slow Operation Threshold

Atlas enables the Atlas-managed slow operation threshold by default. To re-
enable the Atlas-managed slow operation threshold that you previously
disabled:

Atlas CLI

Atlas Administration API

To enable the Atlas-managed slow operation threshold for your project using
the Atlas CLI, run the following command:

    
    
    atlas performanceAdvisor slowOperationThreshold enable [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas performanceAdvisor slowOperationThreshold enable.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Index Considerations

Indexes improve read performance, but a large number of indexes can negatively
impact write performance since indexes must be updated during writes. If your
collection already has several indexes, consider this tradeoff of read and
write performance when deciding whether to create new indexes. Examine whether
a query for such a collection can be modified to take advantage of existing
indexes, as well as whether a query occurs often enough to justify the cost of
a new index.

## Access Performance Advisor

Atlas CLI

Atlas UI

### View Collections with Slow Queries

To return up to 20 namespaces in `<database>.<collection>` format for
collections experiencing slow queries using the Atlas CLI, run the following
command:

    
    
    atlas performanceAdvisor namespaces list [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas performanceAdvisor namespaces list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### View Slow Query Logs

To return query log line items for slow queries that the Performance Advisor
and Query Profiler identify using the Atlas CLI, run the following command:

    
    
    atlas performanceAdvisor slowQueryLogs list [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas performanceAdvisor slowQueryLogs list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### View Suggested Indexes

To return suggested indexes for collections experiencing slow queries using
the Atlas CLI, run the following command:

    
    
    atlas performanceAdvisor suggestedIndexes list [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas performanceAdvisor suggestedIndexes list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

The Performance Advisor displays up to 20 query shapes across all collections
in the cluster and suggested indexes for those shapes. The Performance Advisor
ranks the indexes according to their Impact, which indicates High or Medium
based on the total wasted bytes read. To learn more about index ranking, see
Review Index Ranking.

## Note

To view field values in a sample query in the Performance Advisor, you must be
a user with at least one of the following access levels:

  * `Project Owner` access

  * `Project Data Access Admin` access

Users without the aforementioned access cannot see the field values.

## Index Suggestions

The Performance Advisor ranks the indexes that it suggests according to their
Impact, which indicates High or Medium based on the total wasted bytes read.
To learn more about how the Performance Advisor ranks indexes, see Review
Index Ranking.

To learn how to create indexes that the Performance Advisor suggests, see
Create Suggested Indexes.

### Index Metrics

Each index that the Performance Advisor suggests contains the following
metrics. These metrics apply specifically to queries which would be improved
by the index:

Metric

|

Description  
  
|  
  
Execution Count

|

Number of queries executed per hour which would be improved.  
  
Average Execution Time

|

Current average execution time in milliseconds for affected queries.  
  
Average Query Targeting

|

Average number of documents read per document returned by affected queries. A
higher query targeting score indicates a greater degree of inefficiency. For
more information on query targeting, see Query Targeting.  
  
In Memory Sort

|

Current number of affected queries per hour that needed to be sorted in
memory.  
  
Average Docs Scanned

|

Average number of documents scanned.  
  
Average Docs Returned

|

Average number of documents returned.  
  
Average Object Size

|

Average object size.  
  
### Sample Queries

For each suggested index, the Performance Advisor shows the most commonly
executed query shapes that the index would improve. For each query shape, the
Performance Advisor displays the following metrics:

Metric

|

Description  
  
|  
  
Execution Count

|

Number of queries executed per hour which match the query shape.  
  
Average Execution Time

|

Average execution time in milliseconds for queries which match the query
shape.  
  
Average Query Targeting

|

Average number of documents read for every document returned by matching
queries. A higher query targeting score indicates a greater degree of
inefficiency. For more information on query targeting, see Query Targeting.  
  
Average Docs Scanned

|

Average number of documents scanned.  
  
Average Docs Returned

|

Average number of documents returned.  
  
The Performance Advisor also shows each executed sample query that matches the
query shape, with specific metrics for that query.

### Query Targeting

Each index suggestion includes an Average Query Targeting score indicating how
many documents were read for every document returned for the index's
corresponding query shapes. A score of 1 represents very efficient query
shapes because every document read matched the query and was returned with the
query results. All suggested indexes represent an opportunity to improve query
performance.

### Filter Index Suggestions

By default, the Performance Advisor suggests indexes for all clusters in the
deployment. To only show suggested indexes from a specific collection, use the
Collection dropdown at the top of the Performance Advisor.

You can also adjust the time range the Performance Advisor takes into account
when suggesting indexes by using the Time Range dropdown at the top of the
Performance Advisor.

### Limitations of Index Suggestions

#### Timestamp Format

The Performance Advisor can't suggest indexes for MongoDB databases configured
to use the `ctime` timestamp format. As a workaround, set the timestamp format
for such databases to either `iso8601-utc` or `iso8601-local`. To learn more
about timestamp formats, see mongod --timeStampFormat.

#### Log Size

The Performance Advisor analyzes up to 200,000 of your cluster's most recent
log lines.

#### Log Quantity

If a cluster experiences an activity spike and generates an extremely large
quantity of log messages, Atlas may stop collecting and storing new logs for a
period of time.

## Note

Log analysis rate limits apply only to the Performance Advisor UI, the Query
Profiler UI, and the Access Tracking UI. Downloadable log files are always
complete.

#### Time-Series Collections

The Performance Advisor doesn't provide performance suggestions for time-
series collections.

#### User Feedback

The Performance Advisor includes a user feedback button for Index Suggestions.
Atlas hides this button for serverless instances.

## Create Suggested Indexes

You can create indexes suggested by the Performance Advisor directly within
the Performance Advisor itself. When you create indexes, keep the ratio of
reads to writes on the target collection in mind. Indexes come with a
performance cost, but are more than worth the cost for frequent queries on
large data sets. To learn more about indexing strategies, see Indexing
Strategies.

### Behavior and Limitations

  * You can't create indexes through the Performance Advisor if Data Explorer is disabled for your project. You can still view the Performance Advisor recommendations, but you must create those indexes from `mongosh`.

  * You can only create one index at a time through the Performance Advisor. If you want to create more simultaneously, you can do so using the Atlas UI, a driver, or the shell

  * Atlas always creates indexes for entire database deployments. If you create an index while viewing the Performance Advisor for a single shard in a sharded cluster, Atlas creates that index for the entire sharded cluster.

### Procedure

To create a suggested index:

1

#### For the index you want to create, click Create Index.

The Performance Advisor opens the Create Index dialog and prepopulates the
Fields based on the index you selected.

2

####  _(Optional)_ Specify the index options.

    
    
    { <option1>: <value1>, ... }  
      
  
## Example

The following options document specifies the `unique` option and the `name`
for the index:

    
    
    { unique: true, name: "myUniqueIndex" }  
      
  
3

####  _(Optional)_ Set the Collation options.

Use collation to specify language-specific rules for string comparison, such
as rules for lettercase and accent marks. The collation document contains a
`locale` field which indicates the ICU Locale code, and may contain other
fields to define collation behavior.

## Example

The following collation option document specifies a locale value of `fr` for a
French language collation:

    
    
    { "locale": "fr" }  
      
  
To review the list of locales that MongoDB collation supports, see the list of
languages and locales. To learn more about collation options, including which
are enabled by default for each locale, see Collation in the MongoDB manual.

4

####  _(Optional)_ Enable building indexes in a rolling fashion.

## Important

Rolling index builds succeed only when they meet certain conditions. To ensure
your index build succeeds, avoid the following design patterns that commonly
trigger a restart loop:

  * Index key exceeds the index key limit

  * Index name already exists

  * Index on more than one array field

  * Index on collection that has the maximum number of text indexes

  * Text index on collection that has the maximum number of text indexes

## Note

the Atlas UI doesn't support building indexes with a rolling build for `M0`
free clusters and `M2/M5` shared clusters. You can't build indexes with a
rolling build for serverless instances.

Building indexes in a rolling fashion reduces the performance impact of
building indexes on replica sets and sharded clusters.

To maintain cluster availability:

  * Atlas removes one node from the cluster at a time starting with a secondary.

  * More than one node can go down at a time, but Atlas always keeps a majority of the nodes online.

Atlas automatically cancels rolling index builds that don't succeed on all
nodes. When a rolling index build completes on some nodes, but fails on
others, Atlas cancels the build and removes the index from any nodes that it
was successfully built on.

In the event of a rolling index build cancellation, Atlas generates an
activity feed event and sends a notification email to the project owner with
the following information:

  * Name of the cluster on which the rolling index build failed

  * Namespace on which the rolling index build failed

  * Project that contains the cluster and namespace

  * Organization that contains the project

  * Link to the activity feed event

To learn more about rebuilding indexes, see Build Indexes on Replica Sets.

## Note

The following index options are incompatible with building indexes in a
rolling fashion:

  * unique

  * storageEngine

  * textIndexVersion

  * 2dsphereIndexVersion

If you specify any of these options in the Options pane, Atlas rejects your
configuration with an error message.

5

#### Click Review.

6

#### In the Confirm Operation dialog, confirm your index.

## Important

When an index build completes, Atlas generates an activity feed event and
sends a notification email to the project owner with the following
information:

  * Completion date of the index build

  * Name of the cluster on which the index build completed

  * Namespace on which the index build completed

  * Project containing the cluster and namespace

  * Organization containing the project

  * Link to the activity feed event

← Analyze Slow QueriesReview Index Ranking →

