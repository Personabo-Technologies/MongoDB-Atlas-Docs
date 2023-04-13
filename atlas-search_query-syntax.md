Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Choose an Aggregation Pipeline Stage

Share Feedback

On this page

  * `$search`
  * Definition
  * Fields
  * Behavior
  * Aggregation Variable
  * `$searchMeta`
  * Definition
  * Fields
  * Behavior
  * Metadata Result Types
  * Troubleshooting

## Important

Looking for `$searchBeta`? Use `$search` instead, the official aggregation
stage for running search queries.

Atlas Search queries take the form of an aggregation pipeline stage. This page
describes the following pipeline stages:

  * `$search`

  * `$searchMeta`

## `$search`

### Definition

The `$search` stage performs a full-text search on the specified field or
fields which must be covered by an Atlas Search index.

`$search`

    

A `$search` pipeline stage has the following prototype form:

    
    
    {  
      
      $search: {  
        "index": "<index-name>",  
        "<operator-name>"|"<collector-name>": {  
          <operator-specification>|<collector-specification>  
        },  
        "highlight": {  
          <highlight-options>  
        },  
        "count": {  
          <count-options>  
        },  
        "returnStoredSource": true | false  
      }  
    }  
  
### Fields

The `$search` stage takes a document with the following fields:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`<collector-name>`

|

document

|

Conditional

|

Name of the collector to use with the query. You can provide a document that
contains the collector-specific options as the value for this field. Either
this or `<operator-name>` is required.  
  
`count`

|

document

|

Optional

|

Document that specifies the count options for retrieving a count of the
results. To learn more, see Count Atlas Search Results.  
  
`highlight`

|

document

|

Optional

|

Document that specifies the highlight options for displaying search terms in
their original context.  
  
`index`

|

string

|

Optional

|

Name of the Atlas Search index to use. If omitted, defaults to `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

Atlas Search doesn't returns results if you misspell the index name or if the
specified index doesn't already exist on the cluster.  
  
`<operator-name>`

|

document

|

Conditional

|

Name of the operator to search with. You can provide a document that contains
the operator-specific options as the value for this field. Either this or
`<collector-name>` is required.  
  
`returnStoredSource`

|

boolean

|

Optional

|

Flag that specifies whether to perform a full document lookup on the backend
database or return only stored source fields directly from Atlas Search. If
omitted, defaults to `false`. To learn more, see Return Stored Source Fields.  
  
### Behavior

`$search` must be the first stage of any pipeline it appears in. `$search`
cannot be used in:

  * a view definition

  * a `$facet` pipeline stage

### Aggregation Variable

`$search` returns only the results of your query. The metadata results of your
`$search` query are saved in the `$$SEARCH_META` aggregation variable. You can
use the `$$SEARCH_META` variable to view the metadata results for your
`$search` query. The `$$SEARCH_META` aggregation variable can be used anywhere
after a `$search` stage in any pipeline, but it can't be used after the
`$lookup` or `$unionWith` stage in any pipeline. The `$$SEARCH_META`
aggregation variable can't be used in any subsequent stage after a
`$searchMeta` stage.

## Example

Suppose the following index on the `sample_mflix.movies` collection.

    
    
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
  
The following query searches for movies released near September 01, 2011 using
the `$search` stage. The query includes a:

  * `$project` stage to exclude all fields in the documents except `title` and `released`.

  * `$facet` stage that outputs a:

    * `docs` field with an array of the top `5` search results

    * `meta` field with the value of `$$SEARCH_META` variable

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "near": {  
            "path": "released",  
            "origin": ISODate("2011-09-01T00:00:00.000+00:00"),  
            "pivot": 7776000000  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 0,  
          "title": 1,  
          "released": 1  
        }  
      },  
      { "$limit": 5 },  
      {  
        "$facet": {  
          "docs": [],  
          "meta": [  
            {"$replaceWith": "$$SEARCH_META"},  
            {"$limit": 1}  
          ]  
        }  
      }  
    ])  
  
The query returns the following results:

    
    
    {  
      
      "docs" : [  
        {  
          "title" : "Submarino",  
          "released" : ISODate("2011-09-01T00:00:00Z")  
        },  
        {  
          "title" : "Devil's Playground",  
          "released" : ISODate("2011-09-01T00:00:00Z")  
        },  
        {  
          "title" : "Bag It",  
          "released" : ISODate("2011-09-01T00:00:00Z")  
        },  
        {  
          "title" : "Dos",  
          "released" : ISODate("2011-09-01T00:00:00Z")  
        },  
        {  
          "title" : "We Were Here",  
          "released" : ISODate("2011-09-01T00:00:00Z")  
        }  
      ],  
      "meta" : [  
        { "count" : { "lowerBound" : NumberLong(17373) } }  
      ]  
    }  
  
To learn more about the `$$SEARCH_META` variable and its usage, see:

  * facet

  * count

## `$searchMeta`

## Important

The Atlas Search `$searchMeta` stage is available only on clusters running one
of the following MongoDB versions:

  * MongoDB 4.4.11+

  * MongoDB 5.0.4+

  * MongoDB 6.0+

## Note

To run `$searchMeta` queries over sharded collections, your cluster must run
MongoDB v6.0 or later.

### Definition

The `$searchMeta` stage returns different types of metadata result documents.

`$searchMeta`

    

A `$searchMeta` pipeline stage has the following prototype form:

    
    
    {  
      
      $searchMeta: {  
        "index": "<index-name>",  
        "<collector-name>"|"<operator-name>": {  
          <collector-specification>|<operator-specification>  
        },  
        "count": {  
          <count-options>  
        }  
      }  
    }  
  
### Fields

The `$searchMeta` stage takes a document with the following fields:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`<collector-name>`

|

document

|

Conditional

|

Name of the collector to use with the query. You can provide a document that
contains the collector-specific options as the value for this field. Value
must be `facet` to retrieve a mapping of the defined facet names to an array
of buckets for that facet. To learn more, see facet. You must specify this or
`<operator-name>`.  
  
`count`

|

document

|

Optional

|

Document that specifies the count options for retrieving a count of the
results. To learn more, see Count Atlas Search Results.  
  
`index`

|

string

|

Optional

|

Name of the Atlas Search index to use. If omitted, defaults to `default`.

Atlas Search doesn't return results if you misspell the index name or if the
specified index doesn't already exist on the cluster.  
  
`<operator-name>`

|

document

|

Conditional

|

Name of the operator to search with. You can provide a document that contains
the operator-specific options as the value for this field. You must specify
this or `<collector-name>`. `$searchMeta` returns the default `count` metadata
only.  
  
### Behavior

The `$searchMeta` stage must be the first stage in any pipeline.

### Metadata Result Types

The structure of the metadata results document that is returned by the
`$searchMeta` stage varies based on the type of results. Atlas Search supports
the following result types:

Type

|

Result Structure  
  
|  
  
`count`

|

The count result included in the results indicate whether the count returned
in the results is a total count of the search results, or a lower bound. To
learn more, see Count Results.  
  
`facet`

|

The result to a facet query is a mapping of the defined facet names to an
array of buckets for that facet. To learn more, see Facet Results.  
  
## Troubleshooting

If you are experiencing issues with your Atlas Search `$search` queries, see
Troubleshoot Atlas Search Errors.

← Create and Run Atlas Search QueriesUse Operators and Collectors in Atlas
Search Queries →

