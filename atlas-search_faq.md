Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# FAQ: Atlas Search

Share Feedback

On this page

  * Are there any charges for enabling and using Atlas Search?
  * Can I run partial string matching Atlas Search queries?
  * Can I perform case-insensitive search with the `wildcard` or `regex` operator?
  * Does `storedSource` support case-insensitive collation on fields?
  * Can I use the shard key to run Atlas Search queries on specific shard(s)?
  * Do queries run on primary or secondary nodes?
  * Can I duplicate an index?
  * Does Atlas Search store my entire index in memory?
  * Why is my search index disappearing?
  * Can I restore Atlas Search indexes from Cloud Backup snapshots?
  * Does Atlas Search work with CSFLE encrypting clients?
  * Can I query CSFLE encrypted data?
  * Can I use Atlas Search on time series collections?

## Are there any charges for enabling and using Atlas Search?

No, there are no additional fees or charges for using Atlas Search. However,
you might observe an increase in resource utilization on the cluster,
depending on factors such as the size of the indexed collections or index
definitions.

## Tip

### See also:

  * Atlas Search Overview

  * Atlas Search Index Performance

## Can I run partial string matching Atlas Search queries?

Yes. The following Atlas Search operators support partial string matching
queries:

  * autocomplete

  * wildcard

  * regex

## Tip

### See also:

How to Run Partial Match Atlas Search Queries

## Can I perform case-insensitive search with the `wildcard` or `regex`
operator?

Yes. You can use the wildcard and regex operators with a custom analyzer to
perform a case-insensitive search. You can define a custom analyzer with the
following tokenizer and token filter to perform a wildcard case-insensitive
search:

  * keyword tokenizer

  * lowercase token filter

## Does `storedSource` support case-insensitive collation on fields?

Yes. The Atlas Search storedSource option stores original values. To perform
case-insensitive operations after the `$search` stage on the results returned
using returnStoredSource option, you must set the default collation strength
of your collection to `1` or `2` when you create it, and must not specify a
different collation in your queries and indexes.

## Can I use the shard key to run Atlas Search queries on specific shard(s)?

No, you can't use the shard key to run Atlas Search queries on a specific
shard or a subset of shards. In a sharded cluster environment, Atlas Search
queries are scatter-gather queries that run on all the shards.

## Do queries run on primary or secondary nodes?

By default, queries run on the primary node. You can configure your read
preference or use replica set tags to specify read preference. To learn more,
see Atlas Search Overview.

## Can I duplicate an index?

Yes, you can duplicate your index by performing the following:

1

### Open the Atlas Search index you want to update.

1

#### Navigate to your Search tab.

2

#### On the index you want to copy, click `...` in the Action column.

3

#### Click Edit With JSON Editor.

2

### Copy the index.

3

### Navigate to the Search tab.

4

### Create a new Atlas Search index.

Create a new index with the JSON Editor. Paste the index you copied and click
Create Search Index. You can make any edits you want directly in the JSON
Editor or Visual Index Builder after you create the Atlas Search index.

## Note

### Work in Progress

We are currently working on a solution for this that doesn't require the steps
mentioned above. If you'd like to vote for this feature, or submit your
feedback, see this feedback item.

## Does Atlas Search store my entire index in memory?

No, Atlas Search uses memory for the JVM heap metrics, which stores the
autocomplete and text tokens of your search index. Similar to other database
engines, Atlas Search stores the majority of the index files on the disk,
which benefits from the underlying OS page cache.

## Why is my search index disappearing?

  * Double check that you entered the correct database and collection names. If you enter a non-existent database or collection name, the Atlas UI temporarily builds the index and deletes it shortly after.

  * If you use the `$out` aggregation stage to overwrite your collection, you must delete and recreate your search index, as search indexes are not copied to destination collections. To learn more, see $out Index Constraints.

## Can I restore Atlas Search indexes from Cloud Backup snapshots?

Atlas can restore Atlas Search indexes from a Cloud Backup snapshot only if
both of the following are true:

  * You restore the Cloud Backup snapshot to the same cluster as the source of the backup.

  * The Atlas Search index exists in the cluster at the time of restoration. If you delete the Atlas Search index after the snapshot but before the restoration, Atlas can't restore the Atlas Search index from the snapshot.

Otherwise, you must manually rebuild Atlas Search indexes on the cluster.

## Does Atlas Search work with CSFLE encrypting clients?

Yes, you can use CSFLE encrypting clients to run Atlas Search queries against
data in MongoDB version 6.0 and later.

## Can I query CSFLE encrypted data?

No, you can't query CSFLE encrypted data using Atlas Search.

## Can I use Atlas Search on time series collections?

No, you can't use Atlas Search on time series collections.

← Atlas Search M0 (Free Cluster), M2, and M5 LimitationsAtlas Search Changelog
→

