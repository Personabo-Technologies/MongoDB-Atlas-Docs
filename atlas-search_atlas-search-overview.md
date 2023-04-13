Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Search Overview

Share Feedback

On this page

  * Atlas Search Architecture
  * Atlas Search Indexes
  * Atlas Search Queries
  * Next Steps

MongoDB's Atlas Search allows fine-grained text indexing and querying of data
on your Atlas cluster. It enables advanced search functionality for your
applications without any additional management or separate search system
alongside your database. Atlas Search provides options for several kinds of
text analyzers, a rich query language that uses Atlas Search aggregation
pipeline stages like `$search` and `$searchMeta` in conjunction with other
MongoDB aggregation pipeline stages, and score-based results ranking.

Atlas Search is available on Atlas instances running MongoDB 4.2 or higher
versions only. For certain features, Atlas Search might require a specific
version of MongoDB. The following table lists the Atlas Search features that
require specific MongoDB versions.

Atlas Search Feature

|

MongoDB Version for Feature  
  
|  
  
Facets

|

4.4.11+, 5.0.4+, 6.0+  
  
Facets on Sharded Clusters

|

6.0+  
  
Stored Source Fields

|

4.4.12+, 5.0.6+, 6.0+  
  
$lookup with $search

|

6.0+  
  
$unionWith with $search

|

6.0+  
  
Atlas Search is not supported for time series collections.

## Atlas Search Architecture

The Atlas Search `mongot` Java web process uses Apache Lucene and runs
alongside `mongod` on each node in the Atlas cluster. The `mongot` process:

  1. Creates Atlas Search indexes based on the rules in the index definition for the collection.

  2. Monitors change streams for the current state of the documents and index changes for the collections for which you defined Atlas Search indexes.

  3. Processes Atlas Search queries and returns matching documents.

If you define stored source fields in your Atlas Search index, the `mongot`
process stores the specified fields and, for matching documents, returns the
stored fields directly from `mongot` instead of doing a full document lookup
on the database if you specify the returnStoredSource Option in your query.

### Atlas Search Indexes

Atlas Search index is a data structure that categorizes data in an easily
searchable format. It is a mapping between terms and the documents that
contain those terms. Atlas Search indexes enable faster retrieval of documents
using certain identifiers. You must configure an Atlas Search index to query
data in your Atlas cluster using Atlas Search.

You can create an Atlas Search index on a single field or on multiple fields.
We recommend that you index the fields that you regularly use to sort or
filter your data in order to quickly retrieve the documents that contain the
relevant data at query-time.

When you configure one or more Atlas Search indexes, Atlas enables the
`mongot` process on the nodes in the cluster. Each `mongot` process talks to
the `mongod` on the same node. To create and update search indexes, the
`mongot` process performs collection scans on the backend database and opens
change streams for each index.

You can specify the fields to index using the following methods:

  * Dynamic mappings, which enables Atlas Search to automatically index all the fields of supported types in each document. This takes disk space and might negatively impact cluster performance.

  * Static mappings, which allows you to selectively identify the fields to index.

Atlas Search performs inverted indexing and stores the indexed fields on disk.
An inverted index is a mapping between terms and which documents contain those
terms. Atlas Search indexes contain the term, the `_id`, and other relevant
metadata about the term, such as the position of the term, in the document.

Although the data stored on Atlas Search isn't an identical copy of data from
the collection on your Atlas cluster, Atlas Search indexes still take some
disk space and memory. If you enable the `store` option for fields that
contain How to Index String Fields values or if you configure the stored
source fields in your index, Atlas Search stores an identical copy of the
specified fields on disk, which can take disk space.

Atlas Search provides built-in analyzers for creating indexable terms that
correct for differences in punctuation, capitalization, stop words, and more.
Analyzers apply parsing and language rules to the query. You can also create a
custom analyzer using available built-in character filters, tokenizers, and
token filters. To learn more about the built-in and custom analyzers, see
Process Data with Analyzers.

For text fields, the `mongot` performs the following tasks to create indexable
tokens:

  1. Analysis of the text

  2. Tokenization, which is breaking up of words in a string to indexable tokens

  3. Normalization, such as transforming the text to lower case, folding diacritics, and removing stop words

  4. Stemming, such as ignoring plural and other word forms to index the word in the most reduced form

To learn more about Atlas Search support for other data types, see Data Types
and Data Types. The `mongot` process stores the indexed fields and the `_id`
field on disk per index for the collections on the cluster.

If you change an existing index, Atlas Search rebuilds the index without
downtime. This allows you to continue using the old index for existing and new
queries until the index rebuilding is complete.

If you make changes to the collection for which you defined Atlas Search
indexes, the latest data might not be available immediately for queries.
However, `mongot` monitors the change streams, which allows it to update
stored copies of data, and Atlas Search indexes are eventually consistent.

After you set up an Atlas Search index for a collection, you can run queries
against the indexed fields.

### Atlas Search Queries

Atlas Search queries take the form of an aggregation pipeline stage. Atlas
Search provides `$search` and `$searchMeta` stages, both of which must be the
first stage in the query pipeline. These stages can be used in conjunction
with other aggregation pipeline stages in your query pipeline. To learn more
about these pipeline stages, see Choose an Aggregation Pipeline Stage.

Atlas Search also provides query operators and collectors that you can use
inside the aggregation pipeline stage. The Atlas Search operators allow you to
locate and retrieve matching data from the collection on your Atlas cluster.
The collector returns a document representing the search metadata results.

You can use Atlas Search operators to query terms, phrases, geographic shapes
and points, numeric values, similar documents, synonymous terms, and more. You
can also search using regex and wildcard expressions. The Atlas Search
compound operator allows you to combine multiple operators inside your
`$search` stage to perform a complex search and filter of data based on what
_must_ , _must not_ , or _should_ be present in the documents returned by
Atlas Search. You can use the compound operator to also match or filter
documents in the `$search` stage itself. Running `$match` after `$search` is
less performant than running `$search` with the compound operator.

To learn more about the syntax, options, and usage of the Atlas Search
operators, see Use Operators and Collectors in Atlas Search Queries.

When you run a query, Atlas Search uses the configured read preference to
identify the node on which to run the query. The query first goes to the
MongoDB process, which is `mongod` for a replica set cluster or `mongos` for a
sharded cluster. For sharded clusters, your cluster data is partitioned across
`mongod` instances and each `mongot` knows about the data on the `mongod` on
the same node only. Therefore, you can't run queries that target a particular
shard. `mongos` directs the queries to all shards, making these _scatter
gather_ queries.

The MongoDB process routes the query to the `mongot` on the same node. Atlas
Search performs the search and scoring and returns the document IDs and other
search metadata for the matching results to `mongod`. The `mongod` then
performs a full document lookup implicitly for the matching results and
returns the results to the client.

Atlas Search associates a relevance-based score with every document in the
result set. The relevance-based scoring allows Atlas Search to return
documents in the order from the highest score to the lowest. Atlas Search
scores documents higher if the query term appears frequently in a document and
lower if the query term appears across many documents in the collection. Atlas
Search also supports customizing the relevance-based default score by
boosting, decaying, or other modifying options. To learn more about
customizing the resulting scores, see Customize and Normalize the Score in
Results.

## Next Steps

For hands-on experience creating Atlas Search indexes and running Atlas Search
queries against the sample datasets, try the tutorials in the following pages:

  * Get Started with Atlas Search

  * Atlas Search Tutorials

← What is MongoDB Atlas Search?Atlas Search Best Practices →

