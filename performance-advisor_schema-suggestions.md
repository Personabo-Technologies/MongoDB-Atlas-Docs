Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Improve Your Schema

Share Feedback

On this page

  * Schema Design Patterns
  * Schema Suggestions
  * Limitations of Schema Suggestions

Your schema is the architecture of your cluster, including your collections,
indexes and documents. Consider schema design early in the development
process.

## Note

### Serverless instances

You can't access the Schema Advisor for serverless instances.

## Schema Design Patterns

You can model your schema based on frequently used design patterns. The
_Building with Patterns_ blog series discusses the following frequently used
design patterns.

To read about situations in which arrays work well, see the following design
patterns:

  * Use The Attribute Pattern for handling data with unique combinations of attributes, such as movie data where each movie is released in a subset of countries.

  * Use The Bucket Pattern for handling tightly grouped or sequential data, such as time span data.

  * Use The Polymorphic Pattern for handling differently shaped documents in the same collection, such as athlete records across several sports.

To read about strategies for keeping documents in your working set at a
manageable size, see the following patterns:

  * Use The Extended Reference Pattern to duplicate a frequently-read portion of data from large documents to smaller ones.

  * Use The Subset Pattern to reduce the size of documents with large array fields.

  * Use The Outlier Pattern to handle a few large documents in an otherwise standard collection.

To learn how to incorporate the flexible data model into your schema, see the
following presentations from **MongoDB.live 2020** :

  * Learn about entity relationships in MongoDB and examples of their implementations with Data Modeling with MongoDB.

  * Learn advanced data modeling design patterns you can incorporate into your schema with Advanced Schema Design Patterns.

## Schema Suggestions

Atlas offers two ways to detect common schema design issues and suggests
modifications that follow MongoDB’s best practices:

  * The Performance Advisor provides holistic schema recommendations for your cluster by sampling documents in your most active collections and collections with slow-running queries.

  * The Atlas UI offers schema suggestions for a specific collection by sampling documents in that collection.

To learn more about how to apply the suggestions offered in either the
Performance Advisor or Data Explorer, refer to the following pages:

Schema Improvement

|

Reason for Suggestion  
  
|  
  
Reduce `$lookup` Operations

|

You are running too many `$lookup` operations on your data. Take advantage of
MongoDB's rich schema model to embed related data in a single collection.  
  
Avoid Unbounded Arrays

|

Your documents contain array fields with many elements, which can degrade
query performance.  
  
Remove Unnecessary Indexes

|

You have unnecessary indexes in your collection, which can consume disk space
and degrade write performance.  
  
Reduce the Size of Large Documents

|

You have excessively large documents, which can degrade the performance of
your most frequent queries.  
  
Reduce Number of Collections

|

You have an exceedingly high number of collections in a database, which can
result in unnecessary disk space usage.  
  
Use Atlas Search for Full-Text Search Queries

|

You are executing queries that rely on inefficient regex matching. Take
advantage of Atlas Search queries that use the $search aggregation pipeline
stage.  
  
## Limitations of Schema Suggestions

  * Schema suggestions for a collection are partly driven by a random sampling of documents from that collection. Because this sampling is performed each time your schema is analyzed, you may see different suggestions at different times for the same collection.

  * The Performance Advisor monitors slow queries recognize certain schema issues, namely too many `$lookup` operations and not utilizing an index for case-sensitive regex queries. If a cluster does not consistently receive long-running queries, the Performance Advisor may not suggest all potential improvements for that cluster, or may not show all reasons why an improvement is being suggested.

  * The Performance Advisor analyzes the 20 most active collections based on the output of the `top` command. To see suggestions for a specific collection, view that collection in the Atlas UI.

  * Neither Performance Advisor nor Atlas UI provide schema suggestions for time-series collections.

← Update $text Queries with Atlas Search for Improved Search PerformanceReduce
`$lookup` Operations →

