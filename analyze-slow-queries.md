Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Analyze Slow Queries

Share Feedback

On this page

  * Performance Advisor
  * Query Profiler
  * Real-Time Performance Panel (RTPP)
  * Best Practices for Query Performance

Atlas provides several tools to help analyze slow queries executed on your
clusters. See the following sections for descriptions of each tool. To
optimize your query performance, review the best practices for query
performance.

## Performance Advisor

The Performance Advisor monitors queries that MongoDB considers slow and
suggests new indexes to improve query performance.

You can use the Performance Advisor to review the following information:

  * Index Ranking

  * Drop Index Recommendations

## Query Profiler

The Query Profiler displays slow-running operations and their key performance
statistics. You can explore a sample of historical queries for up to the last
24 hours without additional cost or performance overhead. Before you enable
the Query Profiler, see Considerations.

## Real-Time Performance Panel (RTPP)

The Real-Time Performance Panel identifies relevant database operations,
evaluates query execution times, and shows the ratio of documents scanned to
documents returned during query execution. RTPP is enabled by default.

## Important

### Required Privileges

To enable or disable Real-Time Performance Panel for a project, you must have
the `Project Owner` role for the project.

## Best Practices for Query Performance

To optimize query performance, review the following best practices:

  * Create queries that your current indexes support to reduce the time needed to search for your results.

  * Avoid creating documents with large array fields that require a lot of processing to search and index.

  * Optimize your indexes and remove unused or inefficent indexes. Too many indexes can negatively impact write performance.

  * Consider the suggested indexes from the Performance Advisor with the highest Impact scores and lowest Average Query Targeting scores.

  * Create the indexes that the Performance Advisor suggests when they align with your Indexing Strategies.

  * The Performance Advisor cannot suggest indexes for MongoDB databases configured to use the ctime timestamp format. As a workaround, set the timestamp format for such databases to either iso8601-utc or iso8601-local.

  * Perform rolling index builds to reduce the performance impact of building indexes on replica sets and sharded clusters.

  * Drop unused, redundant, and hidden indexes to improve write performance and free storage space.

← Monitor Your Database DeploymentsMonitor and Improve Slow Queries →

