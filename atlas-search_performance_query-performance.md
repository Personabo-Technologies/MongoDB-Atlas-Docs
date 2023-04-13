Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Search Query Performance

Share Feedback

On this page

  * Query Operators and Query Complexity
  * Performance Monitoring
  * `$match` Aggregation Stage Usage
  * `$sort` Aggregation Stage Usage

## Query Operators and Query Complexity

The complexity level of Atlas Search queries and the type of operators used
can affect database performance. Highly complex queries with multiple clauses
are resource-intensive, as are queries which use the regex (regular
expression) operator.

Atlas Search queries are ranked by score. Queries that return a large number
of results are more computationally intensive because they must keep track of
all the scores for the result set.

## Performance Monitoring

You can monitor your Atlas cluster and view charts with performance statistics
on the Atlas Metrics tab. These metrics can help you see how Atlas Search
queries and index building affect your cluster's performance. To learn more,
see Review Atlas Search Metrics.

Atlas might trigger some Atlas alerts when:

  * Atlas Search queries your database deployments, which can impact Atlas performance metrics, such as the query targeting metrics.

## Note

The changestream cursors that the Atlas Search process (`mongot`) uses for
replication can contribute to the query targeting ratio and trigger query
targeting alerts if the ratio is high.

  * Atlas Search replicates data from MongoDB, which contributes to the metrics measured in Atlas, such as the number of getmore operations.

## Note

If your cluster's resources are stretched or near the limits of acceptable
performance, consider upgrading to a larger cluster tier before implementing
Atlas Search functionality.

## `$match` Aggregation Stage Usage

Using a $match aggregation pipeline stage after a $search stage can
drastically slow down query results. If possible, design your `$search` query
so that all necessary filtering occurs in the `$search` stage to remove the
need for a `$match` stage. The Atlas Search compound operator is helpful for
queries that require multiple filtering operations. If you must use the
`$match` stage in your aggregation pipeline, consider using the storedSource
option to store only the fields that your `$match` condition needs. You can
then use the returnStoredSource option to retrieve stored fields.

## Tip

### See also:

  * Storing Source Fields

  * $match Example

## `$sort` Aggregation Stage Usage

Using a $sort aggregation pipeline stage after a $search stage can drastically
slow down query results. If possible, design your `$search` query so that all
necessary sorting occurs in the `$search` stage to remove the need for a
`$sort` stage. In general, the Atlas Search compound operator is helpful for
queries that require multiple sorting operations. To sort documents based on a
numeric, date, or geo field, consider using the Atlas Search near operator.
Alternatively, you can use the storedSource option to store only the fields
that you need for `$sort` on Atlas Search and use the returnStoredSource
option to retrieve stored fields.

## Tip

### See also:

  * Storing Source Fields

  * $sort Example

← Atlas Search Index PerformanceFix Atlas Search Issues →

