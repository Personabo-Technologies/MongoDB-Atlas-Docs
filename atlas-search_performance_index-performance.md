Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Search Index Performance

Share Feedback

On this page

  * Resource Requirements
  * Index Size and Configuration
  * Considerations
  * Creating and Updating an Atlas Search Index
  * Eventual Consistency and Indexing Latency
  * Document Mapping Explosions
  * Storing Source Fields
  * Scaling Considerations
  * Atlas Search Upgrade
  * Scaling Up Indexing Performance

## Resource Requirements

### Index Size and Configuration

## Important

If you create an Atlas Search index for a collection that has or will soon
have more than two billion documents, you must shard your cluster.

When you create an Atlas Search index, field mapping defaults to dynamic,
which means that Atlas Search dynamically indexes all the datatypes that can
be dynamically indexed in your collection. Other options such as enabling
highlights can also result in your index taking up more disk space. You can
reduce the size and performance footprint of your Atlas Search index by:

  * Specifying a custom index definition to narrow the amount and type of data that is indexed.

  * Setting the `store` option to `false` when specifying a string type in an index definition.

## Note

Some limitations apply to Atlas Search on `M0`, `M2`, and `M5` clusters only.
To learn more, see Atlas Search Free and Shared Tier Limitations.

#### Considerations

Some index configuration options can lead to indexes that take up a
significant proportion of your disk space. In some cases, your index could be
many times larger than the size of your data. Although this is expected
behavior, it's important to be aware of the following indexing-intensive
features:

##### Autocomplete

The How to Index Fields for Autocompletion Atlas Search field type can cause
large indexes, especially in the following cases:

  * Using `nGram` tokenization.

  * Setting a wide `minGrams` to `maxGrams` range.

  * Setting a `minGram` value of `1` on a collection with millions of documents.

##### Embedded Documents

Atlas Search doesn't support indexing more than two billion index objects,
where each indexed embedded document counts as a single object. Using the
`embeddedDocuments` field type can result in indexing objects over this limit,
which causes an index to transition to a failed state. If your collection has
large arrays that might generate two billion objects, you must shard any
clusters that contain indexes with the `embeddedDocuments` type.

##### `multi` Analyzers

Using a `multi` analyzer to analyze the same field multiple different ways can
cause large indexes, especially when analyzing fields with very long values.

##### Synonym Collections

Inserts and updates to a synonym source collection are fast only if the
synonym source collection is small. For best performance, we recommend
batching inserts and updates to synonym source collections.

A synonym mapping definition doesn't require additional disk space aside from
the disk space utilized by the synonym collection in the database. However,
synonym mappings create artifacts in memory and therefore, for synonym
collections with many documents, Atlas Search creates artifacts that occupy
more memory.

### Creating and Updating an Atlas Search Index

Creating an Atlas Search index is resource-intensive. The performance of your
Atlas cluster may be impacted while the index builds.

Atlas replicates all writes on the collection. This means that for each
collection with Atlas Search indexes, the writes are amplified to the amount
of Atlas Search indexes defined for that collection.

In some instances, your Atlas Search index must be rebuilt. Rebuilding the
Atlas Search index also consumes resources and may affect database
performance. Atlas Search automatically rebuilds the index only in the event
of:

  * Changes to the index definition

  * Atlas Search version updates that include breaking changes

  * Hardware-related problems such as index corruption

## Note

Atlas Search supports no-downtime indexing, which means you can continue to
run search queries while Atlas Search rebuilds your index. Atlas Search keeps
your old index up-to-date while the new index is being built. We recommend
allocating _free_ disk space equal to 125% of the disk space used by your old
index for this operation. You can view the amount of disk space currently used
by your index in the Search Disk Space Used metric.

If your index rebuild fails due to insufficient disk space, we recommend that
you temporarily expand your cluster capacity to meet the increased demand. You
can make this change manually as described in Fix Storage Issues, even for
clusters with autoscaling enabled.

Once Atlas Search rebuilds the index, the old index is automatically replaced
without any further action from your side.

### Eventual Consistency and Indexing Latency

Atlas Search supports eventual consistency and does not provide any stronger
consistency guarantees. This means that data inserted into a MongoDB
collection and indexed by Atlas Search will not be available immediately for
`$search` queries.

Atlas Search reads data from MongoDB change streams and indexes that data in
an asynchronous process. This process is typically very fast, but may
sometimes be impacted by replication latency, system resource availability,
and index definition complexity.

### Document Mapping Explosions

Mapping explosions occur when Atlas Search indexes a document with arbitrary
keys and you have a dynamic mapping. The `mongot` process might consume
increasing amounts of memory and could crash. If you add too many fields to an
index, mapping explosions can occur. To address this issue, you can upgrade
your cluster or use a static mapping that does not index all fields in your
data.

When searching over fields using a wildcard path, design your search to use a
tuple-like schema. If you perform a wildcard path search that uses a key-value
schema, Atlas Search indexes each key as its own field, which can cause
mapping explosions.

## Example

An example of a key-value schema is as follows:

    
    
    ruleBuilder: {  
      
      ruleName1: <data>,  
      ruleName2: <data>,  
      .....  
      ruleName1025: <data>  
    }  
  
An example of the same data restructured to use a tuple-like schema is as
follows:

    
    
    {  
      
      ruleBuilder: [  
        {name: ruleName1, data: <data>},  
        {name: ruleName2, data: <data>},  
        ...  
        {name: ruleName1025, data: <data>}  
      ]  
    }  
  
### Storing Source Fields

You can configure fields to store on Atlas Search and improve performance of
subsequent aggregation pipeline stages like `$sort`, `$match`, `$group`, and
`$skip`. Use this optimization if your original documents and matched dataset
are so large that a full data lookup is inefficient. To learn more about
storing specific fields on Atlas Search and returning those stored fields
only, see Define Stored Source Fields in Your Atlas Search Index and Return
Stored Source Fields.

We recommend storing only the minimum number of fields required for subsequent
stages. If necessary, you can use `$lookup` at the end of the pipeline stage
to retrieve entire documents as shown in the Examples. Storing unnecessary
fields increases disk utilization and could negatively impact performance
during indexing and querying.

## Scaling Considerations

### Atlas Search Upgrade

Atlas Search is deployed on your Atlas cluster. When a new version of Atlas
Search is deployed, your Atlas cluster might experience brief network failures
in returning query results. To mitigate issues during deployment and minimize
impact to your application, consider the following:

  * Implement retry logic in your application.

  * Configure Atlas maintenance windows.

To learn more about the changes in each release, see Atlas Search Changelog.

### Scaling Up Indexing Performance

You can scale up your initial sync and steady state indexing for an Atlas
Search index by upgrading your cluster to a higher tier with more cores. Atlas
Search uses a percentage of all available cores to run both initial sync and
steady state indexing and performance improves as new cores are made available
by upgrading your cluster.

← Tune Atlas Search PerformanceAtlas Search Query Performance →

