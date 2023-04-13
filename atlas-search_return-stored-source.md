Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return Stored Source Fields

Share Feedback

On this page

  * Syntax
  * Behavior
  * Sample Use
  * Examples

If you configured the storedSource option in the index definition for a
collection, Atlas Search stores the specified fields on `mongot`. You can use
the `returnStoredSource` boolean option in your Atlas Search queries to
retrieve only those fields, rather than fetching full documents from the
collection.

By default, Atlas Search performs full document lookup implicitly on the
backend database after Atlas Search matches documents for the query. This
lookup could significantly degrade performance for subsequent aggregation
pipeline stages that fetch all matched dataset from `$search` stage (such as
`$sort`, `$group`) or filter a large part of it (such as `$match`, `$skip`).
If you configured the `storedSource` option, you can use the
`returnStoredSource` option to retrieve only parts of the documents directly
stored on Atlas Search and avoid full document lookup on the database. This
allows you to perform most database-side filtering operations on documents
with a minimum number of fields. You can then retrieve all the fields from the
documents at a later stage in the pipeline using `$lookup`.

## Note

  * `returnStoredSource` is only available on Atlas clusters running MongoDB 4.4 and later.

  * For sharded collections, `$lookup` is only available on Atlas clusters running MongoDB 5.1 and later.

## Syntax

`returnStoredSource` has the following syntax in your queries:

    
    
    {  
      
      $search: {  
        "<operator>": {  
          <operator-specification>  
        },  
        "returnStoredSource": true | false // optional, defaults to "false"  
      }  
    }  
  
To learn more about query syntax, see `$search`.

## Behavior

The `returnStoredSource` boolean option specifies whether Atlas Search must
perform a full document lookup on the database or return the stored fields
directly from Atlas Search. You can use the `returnStoredSource` option only
if your index definition includes the configuration for storing fields on
Atlas Search. To learn more about storing fields on Atlas Search, see Review
Atlas Search Index Syntax and Define Stored Source Fields in Your Atlas Search
Index.

You can set one of the following values for the `returnStoredSource` option:

  * `true` \- to return only stored source fields directly from Atlas Search

  * `false` \- to do an implicit full document lookup on the backend database (default)

If you run Atlas Search queries with the `returnStoredSource` boolean option
set to `true`:

  * Atlas Search returns an empty document if the document doesn't include the fields configured for storing.

  * Atlas Search returns errors if the index definition doesn't include the Stored Source configuration.

  * Atlas Search might return stale data due to a replication lag.

  * Atlas Search might return duplicate data on sharded clusters.

If you perform a high volume and rate of data insert and update operations for
your collection on the backend database, Atlas Search might return stale data
because the data stored on `mongot` might not be current due to a replication
lag. You can view the approximate number of milliseconds that Atlas Search is
behind in replicating changes from the oplog of `mongod` in the Atlas UI. To
learn more, see Review Atlas Search Metrics.

If there are orphaned documents during chunk migration, Atlas Search might
return duplicate documents for queries against sharded cluster.

## Sample Use

If your `$search` stage discards a lot of the results and you need to perform
implicit document lookup on your database, we recommend using the
`returnStoredSource` option. You can store fields required for sorting or
filtering and use `returnStoredSource` option at query time to perform the
following actions:

  1. Intermediate operations on partial documents returned by Atlas Search

  2. `$lookup` at the end of the pipeline if full documents are needed.

## Important

For efficiency, configure only a minimum number of fields for storage on Atlas
Search. Use this option if your documents are large enough to cause issues
during lookup.

## Examples

The examples in this section use the `sample_mflix.movies` collection. The
examples show how to do a sort or match on the documents that Atlas Search
returns after the `$search` stage and then lookup documents on the database.

Sort Example

Match Example

  1. Create the index using the following index definition. The index definition for the collection specifies the following fields:

    * Index `title` field

    * Store `year` and `title` fields
    
        {  
      
      "mappings": {  
        "fields": {  
          "title": {  
            "type": "string"  
          }  
        }  
      },  
      "storedSource": {  
        "include": [  
          "year",  
          "title"  
        ]  
      }  
    }  
  
  2. Run the following query against the collection:
    
        db.movies.aggregate([  
      
      {  
        // search and output documents  
        $search: {  
          "text": {  
            "query": "baseball",  
            "path": "title"  
          },  
          "returnStoredSource": true // return stored fields only  
        }  
      },  
      // fetch all matched dataset from $search stage and sort it  
      {  
        $sort: {"year": 1, "title": 1}  
      },  
      // discard everything except top 10 results  
      {  
        $limit: 10  
      },  
      // perform full document lookup for top 10 documents only  
      {  
        $lookup: {  
          from: "movies", localField: "_id", foreignField: "_id", as: "document"  
        }  
      }  
    ])  
  
The query returns the following documents:

    
        1| [  
    |  
    2|   {  
    3|     _id: ObjectId("573a1399f29313caabced370"),  
    4|     title: 'Mr. Baseball',  
    5|     year: 1992,  
    6|     document: [  
    7|       { ... } // full document returned by $lookup  
    8|     ]  
    9|   },  
    10|   {  
    11|     _id: ObjectId("573a1399f29313caabcee1aa"),  
    12|     title: 'Baseball',  
    13|     year: 1994,  
    14|     document: [  
    15|       { ... } // full document returned by $lookup  
    16|     ]  
    17|   }  
    18| ]  
  

← Explain Timing BreakdownCount Atlas Search Results →

