Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# embeddedDocument

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Behavior
  * Limitations
  * Examples

## Note

The Atlas Search embeddedDocuments index option, embeddedDocument operator,
and `embedded` scoring option are in preview. When an Atlas Search index on a
replica set or single MongoDB shard reaches Lucene's two billion document
limit, Atlas Search doesn't index new documents or apply updates to existing
documents for that index. A solution to accommodate this limitation will be in
place when this feature is generally available. To troubleshoot any issues
related to using this feature, contact Support.

## Definition

`embeddedDocument`

    

The `embeddedDocument` operator is similar to $elemMatch operator. It
constrains multiple query predicates to be satisfied from a single element of
an array of embedded documents. `embeddedDocument` can be used only for
queries over fields of type How to Index Fields in Arrays of Objects and
Documents.

## Syntax

`embeddedDocument` has the following syntax:

    
    
    {  
      
      "embeddedDocument": {  
        "path": "<path-to-field>",  
        "operator": { <operator-specification> },  
        "score": { <score-options> }  
      }  
    }  
  
## Options

`embeddedDocument` uses the following options to construct a query:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`operator`

|

object

|

Operator to use to query each document in the array of documents that you
specify in the `path`. The moreLikeThis operator is not supported.

|

Required  
  
`path`

|

string

|

Indexed How to Index Fields in Arrays of Objects and Documents type field to
search. The specified field must be a parent for all operators and fields
specified using the `operator` option. See Path Construction for more
information.

|

Required  
  
`score`

|

object

|

Score to assign to matching search results. You can use the `embedded` scoring
option to configure scoring options. If you omit this option or use another
scoring option, `embeddedDocument` operator uses the default aggregation
strategy, `sum`, for combining scores of embedded document matches. To learn
more, see Customize and Normalize the Score in Results.

|

Optional  
  
## Behavior

When you query embedded documents in arrays using the `embeddedDocument`
operator, Atlas Search evaluates and scores the operator query predicates at
different stages of query execution. Atlas Search:

  1. Evaluates each embedded document in the array independently.

  2. Combines the scores of matching results as configured using the `embedded` option, or scores by summing the scores of matching results if you don't specify an `embedded` score option.

  3. Joins the matching results with the parent document if other query predicates are specified through the compound operator.

## Note

For string faceting, Atlas Search counts string facets once for each document
in the result set. For an example of this behavior, see Examples.

## Limitations

You can't highlight on queries inside the `embeddedDocument` operator.

## Examples

The following examples use the `sample_supplies.sales` collection in the
sample dataset. These examples use the following index definition on the
collection:

    
    
    {  
      
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "items": {  
            "dynamic": true,  
            "type": "embeddedDocuments"  
          },  
          "purchaseMethod": {  
            "type": "stringFacet"  
          }  
        }  
      }  
    }  
  
Basic Example

Facet Example

The following query searches the collection for items tagged `school` with a
preference for items named `backpack`. Atlas Search scores the results in
descending order based on the average (arithmetic mean) score of all matching
embedded documents. The query includes a `$limit` stage to limit the output to
`5` documents and a `$project` stage to:

  * Exclude all fields except `items.name` field

  * Add a field named `score`

    
    
    1| db.sales.aggregate({  
    |  
    2|   "$search": {  
    3|     "embeddedDocument": {  
    4|       "path": "items",  
    5|       "operator": {  
    6|         "compound": {  
    7|           "must": [{  
    8|             "text": {  
    9|               "path": "items.tags",  
    10|               "query": "school"  
    11|             }  
    12|           }],  
    13|           "should": [{  
    14|             "text": {  
    15|               "path": "items.name",  
    16|               "query": "backpack"  
    17|             }  
    18|           }]  
    19|         }  
    20|       },  
    21|       "score": {  
    22|         "embedded": {  
    23|           "aggregate": "mean"  
    24|         }  
    25|       }  
    26|     }  
    27|   }  
    28| },  
    29| {  
    30|   $limit: 5  
    31| },  
    32| {  
    33|   $project: {  
    34|     "_id": 0,  
    35|     "items.name": 1,  
    36|     "items.tags": 1,  
    37|     "score": { $meta: "searchScore" }  
    38|   }  
    39| })  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        items: [ {  
          name: 'backpack',  
          tags: [ 'school', 'travel', 'kids' ]  
        } ],  
        score: 1.2907354831695557  
      },  
      {  
        items: [ {  
          name: 'envelopes',  
          tags: [ 'stationary', 'office', 'general' ]  
        },  
        {  
          name: 'printer paper',  
          tags: [ 'office', 'stationary' ]  
        },  
        {  
          name: 'backpack',  
          tags: [ 'school', 'travel', 'kids' ]  
        } ],  
        score: 1.2907354831695557  
      },  
      {  
        items: items: [ {  
          name: 'backpack',  
          tags: [ 'school', 'travel', 'kids' ]  
        } ],  
        score: 1.2907354831695557  
      },  
      {  
        items: [ {  
          name: 'backpack',  
          tags: [ 'school', 'travel', 'kids' ]  
        } ],  
        score: 1.2907354831695557  
      },  
      {  
        items: [ {  
          name: 'backpack',  
          tags: [ 'school', 'travel', 'kids' ]  
        } ],  
        score: 1.2907354831695557  
      }  
    ]  
  
← compoundequals →

