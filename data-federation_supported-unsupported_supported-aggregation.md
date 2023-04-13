Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Supported Aggregation Pipeline Stages and Operators

Share Feedback

This page describes the MongoDB aggregation pipeline stages and operators that
Atlas Data Federation supports.

## Note

By default, Atlas Data Federation does not return documents in any specific
order for queries on Data Federations for S3 data stores. Atlas Data
Federation reads the partitions concurrently and the underlying storage
response order determines which documents Atlas Data Federation returns first,
unless you define order using `$sort` in your query. For example, if you run
the same `findOne()` query twice, you could see different documents, and if
you use `$skip`, different documents might be skipped if `$sort` is not used
in the query.

## Supported and Unsupported Aggregation Pipeline Stages

Atlas Data Federation supports all the aggregation pipeline stages except the
following:

  * `$indexStats`

  * `$listSessions`

  * `$listLocalSessions`

  * `$planCacheStats`

For the following stages in Atlas Data Federation queries, Atlas Data
Federation introduces an alternate syntax, includes a caveat, or deviates from
server. See the _Description_ column for details.

Pipeline Stage

|

Description  
  
|  
  
`$group`

|

Groups input documents by the specified `_id` expression and for each distinct
grouping, outputs a document. Atlas Data Federation doesn't support empty
string keys for the accumulator fields.

## Example

The following is **not** supported:

    
    
    | {  
      
                  "$group" : {  
                          "_id" : "$representationType",  
                          "" : {  
                                  "$sum" : NumberInt(1)  
                          }  
                  }  
          }  
  
`$lookup`

|

Performs a left outer join to a collection in the same database. Atlas Data
Federation provides syntax for joining collections from different databases
also. See `$lookup` for more information.  
  
`$match`

|

Filters the documents to pass only the documents that match the specified
condition(s) to the next pipeline stage. Atlas Data Federation supports
`$match`. Note that the partition attributes for selecting specific files on
S3 are only optimized for the following aggregation pipeline operators: $eq,
$gt, $lt, $gte, $lte, $ne, $and, $or.  
  
`$merge`

|

Writes the results of the aggregation pipeline to a specified collection.
Atlas Data Federation provides alternate syntax for the required `into` field
to allow writes to an Atlas cluster. To learn more, see `$merge`.  
  
`$out`

|

Takes the documents returned by the aggregation pipeline and writes them to a
specified collection. Atlas Data Federation provides alternate syntax for
writing to S3 and Atlas cluster.

To use $out to write to a collection in a different database on the same Atlas
cluster, your Atlas cluster must be on MongoDB version 4.4 or later.

See `$out` for more information.  
  
`$sample`

|

Randomly selects the specified number of documents from its input. Atlas Data
Federation supports `$sample`, but does not provide a truly random sample and
returns the first set of documents that it finds.  
  
`$skip`

|

Skips over the specified number of documents that pass into the stage and
passes the remaining documents to the next stage in the pipeline. Atlas Data
Federation supports `$skip`, but this does not reduce data scan because Data
Federation accesses all partitions that correspond to your query.  
  
## Supported Aggregation Pipeline Operators

Atlas Data Federation supports all the aggregation pipeline operators.
However, Atlas Data Federation supports all the geospatial query operators and
the following evaluation query operators only in queries on collections that
are mapped to an Atlas cluster data store.

## Note

Atlas Data Federation doesn't include a server-side JavaScript engine. So,
Atlas Data Federation doesn't support operators such as $where, $function, and
$accumulator that require server-side scripting enabled.

Pipeline Stage

|

Description  
  
|  
  
`$geoNear`

|

Outputs documents in order of nearest to farthest from a specified point.
Atlas Data Federation supports `$geoNear` in queries on virtual collections
that are mapped to one or more Atlas collections. Atlas Data Federation
doesn't support `$geoNear` for S3 or HTTP federated database instance stores.

See Querying Data in Your Atlas Cluster for more information.  
  
`$graphLookup`

|

Performs a recursive search on a collection. Atlas Data Federation supports
`$graphLookup` in queries on virtual collections that are mapped to one Atlas
collection only. Atlas Data Federation doesn't support `$graphLookup` for:

  * S3 or HTTP stores.

  * Queries on virtual collections that are mapped to multiple Atlas collections.

See Querying Data in Your Atlas Cluster for more information.  
  
`$search`

|

Performs a full-text search on the content of the fields covered by an Atlas
Search index.  
  
$text

|

Performs a text search on the content of the fields indexed with a text index.  
  
$where

|

Passes either a string containing a JavaScript expression or a full JavaScript
function to the query system.  
  
← Storage Configuration Commands`$collStats` →

