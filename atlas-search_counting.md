Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Count Atlas Search Results

Share Feedback

On this page

  * Syntax
  * Options
  * Count Results
  * `SEARCH_META` Aggregation Variable
  * Examples

The Atlas Search `count` option adds a field to the metadata results document
that displays a count of the search results for the query. You can use `count`
to determine the size of the result set. You can use it in the $search or
`$searchMeta` stage. You must use it in conjuction with the operators or
collectors to display either the total number of documents or a lower bound on
the number of documents that match the query.

## Note

To use `count` option over sharded collections, your cluster must run MongoDB
v6.0 or higher.

MongoDB recommends using `count` with the `$searchMeta` stage to retrieve
metadata results only for the query. To retrieve metadata results and query
results using the `$search` stage, you must use the `$$SEARCH_META` variable.
To learn more, see `SEARCH_META` Aggregation Variable.

## Note

Atlas Search doesn't include the `count` results in the results for queries
run with `count` in explain mode.

## Syntax

`count` has the following syntax:

    
    
    {  
      
      "$searchMeta"|"$search": {  
        "index": "<index name>", // optional, defaults to "default"  
        "<operator>": {  
          <operator-specifications>  
        },  
        "count": {  
          "type": "lowerBound"|"total",  
          "threshold": <number-of-documents> //optional  
        }  
      }  
    }  
  
## Options

Field

|

Type

|

Description

|

Required?  
  
|||  
  
`type`

|

string

|

Type of count of the documents in the result set. Value can be one of the
following:

  * `lowerBound` \- for a lower bound count of the number of documents that match the query. You can set the `threshold` for the lower bound number.

  * `total` \- for an exact count of the number of documents that match the query. If the result set is large, Atlas Search might take longer than for `lowerBound` to return the count.

If omitted, defaults to `lowerBound`.

|

no  
  
`threshold`

|

int

|

Number of documents to include in the exact count if `type` is `lowerBound`.
If omitted, defaults to `1000`, which indicates that any number up to `1000`
is an exact count and any number above `1000` is a rough count of the number
of documents in the result.

|

no  
  
## Count Results

The count document included in the results document contains the following
integer fields:

Option

|

Description  
  
|  
  
`lowerBound`

|

Lower bound for this result set. This is returned only when a count of type
`lowerBound` is requested.  
  
`total`

|

Total count for this result set. This is returned only when a count of type
`total` is requested.  
  
## `SEARCH_META` Aggregation Variable

When you run your query using the `$search` stage, Atlas Search stores the
metadata results in the `$$SEARCH_META` variable and returns only the search
results. You can use the `$$SEARCH_META` variable in all the supported
aggregation pipeline stages to view the metadata results for your `$search`
query.

MongoDB recommends using the `$$SEARCH_META` variable only if you need both
the search results and the metadata results. Otherwise, use the:

  * `$search` stage for just the search results.

  * `$searchMeta` stage for just the metadata results.

## Example

Suppose an index on the `released` field in the `sample_mflix.movies`
collection:

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "released": {  
            "type": "date"  
          }  
        }  
      }  
    }  
  
The following query searches for movies released near September 01, 2011 in
the `movies` collection. The query requests a total count of the results. The
query includes a:

  * `$project` stage to exclude all fields except `title` and `released` from the documents and to include the metadata results stored in the `$$SEARCH_META` variable as the value of a field named `meta`.

  * `$limit` stage to limit the output to `2` documents.

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "near": {  
            "path": "released",  
            "origin": ISODate("2011-09-01T00:00:00.000+00:00"),  
            "pivot": 7776000000  
          },  
            "count": {  
              "type": "total"  
            }  
          }  
        },  
        {  
          "$project": {  
            "meta": "$$SEARCH_META",  
            "title": 1,  
            "released": 1  
          }  
        },  
        {  
          "$limit": 2  
        }  
      ])  
  
Atlas Search returns the following results for the query:

    
    
    {  
      
      "_id" : ObjectId("573a13c3f29313caabd6b025"),  
      "title" : "Submarino",  
      "released" : ISODate("2011-09-01T00:00:00Z"),  
      "meta" : {  
        "count" : { "total" : NumberLong(23026) }  
      }  
    }  
    {  
      "_id" : ObjectId("573a13c7f29313caabd748f7"),  
      "title" : "Devil's Playground",  
      "released" : ISODate("2011-09-01T00:00:00Z"),  
      "meta" : {  
        "count" : { "total" : NumberLong(23026) }  
      }  
    }  
  
To learn more about the results, see Count Results.

## Examples

The following example uses an index on the `year` field in the
`sample_mflix.movies` collection:

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "year": {  
            "type": "number"  
          }  
        }  
      }  
    }  
  
lowerBound Example

total Example

The following query searches for the movies between the years `2010` and
`2015` in the `movies` collection. The query requests a lower bound count of
the results:

    
    
    db.movies.aggregate([  
      
      {  
        "$searchMeta": {  
          "range": {  
            "path": "year",  
            "gte": 2010,  
            "lte": 2015  
          },  
          "count": {  
            "type": "lowerBound"  
          }  
        }  
      }  
    ])  
  
Atlas Search returns the following results:

    
    
    { "count" : { "lowerBound" : NumberLong(1001) } }  
      
  
← Return Stored Source FieldsRun Atlas Search Queries →

