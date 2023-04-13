Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# queryString

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Examples
  * Basic Examples
  * Advanced Examples

## Definition

`queryString`

    

The `queryString` operator supports querying a combination of indexed fields
and values.

## Syntax

`queryString` has the following syntax:

    
    
    1| {  
    |  
    2|   "$search": {  
    3|      "index": <index name>, // optional, defaults to "default"  
    4|      "queryString": {  
    5|         "defaultPath": "<default-field-to-search>",  
    6|         "query": "(<field-to-search>: (<search-values>) AND|OR (<search-values>)) AND|OR (<search-values>)"  
    7|      }  
    8|   }  
    9| }  
  
## Options

`queryString` uses the following terms to construct a query:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`defaultPath`

|

string

|

The indexed field to search by default. Atlas Search only searches the field
in `defaultPath` if you omit the field to search in the `query`.

|

yes  
  
`query`

|

string

|

One or more indexed fields and values to search. Fields and values are colon-
delimited. For example, to search the `plot` field for the string `baseball`,
use `plot:baseball`. The following operators are available to combine multiple
search criteria:

You can combine the fields and values using the following:

|

|  
  
|  
  
`AND`

|

Indicates `AND` boolean operator. All search values must be present for a
document to be included in the results.  
  
`OR`

|

Indicates `OR` boolean operator. At least one of the search value must be
present for a document to be included in the results.  
  
`NOT`

|

Indicates `NOT` boolean operator. Specified search value must be absent for a
document to be included in the results.  
  
`()`

|

Delimiters for subqueries. Use the parentheses to group fields and values to
search.  
  
## Tip

### See also:

Examples for some sample queries that use the operators and delimiters to
search the sample `movies` collection.

yes  
  
`score`

|

object

|

The score assigned to matching search results. You can modify the score using
the following options:

  * `boost`: multiply the result score by the given number.

  * `constant`: replace the result score with the given number.

For information on using `score` in your query, see Customize and Normalize
the Score in Results.

|

no  
  
## Examples

The following examples use the `movies` collection in the `sample_mflix`
database. If you have the sample dataset on your cluster, you can create the
Atlas Search `default` index and run the example queries on your cluster.

### Basic Examples

AND OR Example

AND NOT Example

AND Example

OR AND Example

The following example uses the `queryString` operator to query for movies with
the title `Rocky` and either `IV`, `4`, or `Four`.

## Example

The following query searches for the combination of `Rocky` and either `IV`,
`4`, or `Four` at path `title` in the `movies` collection. In the following
query, a field is specified in the `defaultPath`, but no fields are specified
in the `query`. The query includes a `$project` stage to exclude all fields
except `title`.

    
    
    1| db.movies.aggregate([  
    |  
    2|    {  
    3|       $search: {  
    4|          "queryString": {  
    5|             "defaultPath": "title",  
    6|             "query": "Rocky AND (IV OR 4 OR Four)"  
    7|          }  
    8|       }  
    9|    },  
    10|    {  
    11|       $project: {  
    12|          "_id": 0,  
    13|          "title": 1  
    14|       }  
    15|    }  
    16| ])  
  
For this query, Atlas Search performs a search at `defaultPath` because there
are no fields in the `query`. It returns the following results:

    
    
    { "title" : "Rocky IV" }  
      
  
### Advanced Examples

The following example uses the `queryString` operator to query for movie plots
that contain the terms `captain`, `kirk`, and `chess`. This example shows how
different grouping of the same search terms using parentheses can result in
different documents to be included in the search results.

## Example

The following queries search for a combination of the terms, `captain`,
`kirk`, and `chess` in the `plot` field. Each query returns a different result
depending on how the search terms are grouped.

The queries also includes a `$project` stage to:

  * Exclude all fields except `title`, `plot`, and `fullpath`

  * Add a field named `score`

Example 1

Example 2

The following query searches for `chess` and either `captain` or `kirk` in the
`plot` field.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|        "queryString": {  
    5|           "defaultPath": "fullplot",  
    6|           "query": "plot:(captain OR kirk) AND chess"  
    7|        }  
    8|     }  
    9|   },  
    10|   {  
    11|     $project: {  
    12|        "_id": 0,  
    13|        "title": 1,  
    14|        "plot": 1,  
    15|        "fullplot": 1,  
    16|        score: { $meta: "searchScore" }  
    17|     }  
    18|   }  
    19| ])  
  
This query returns the following results:

    
    
    {  
      
     "fullplot" : "When the crew of the Enterprise is called back home, they find an unstoppable force of terror from within their own organization has detonated the fleet and everything it stands for, leaving our world in a state of crisis. With a personal score to settle, Captain Kirk leads a manhunt to a war-zone world to capture a one-man weapon of mass destruction. As our heroes are propelled into an epic chess game of life and death, love will be challenged, friendships will be torn apart, and sacrifices must be made for the only family Kirk has left: his crew.",  
     "plot" : "After the crew of the Enterprise find an unstoppable force of terror from within their own organization, Captain Kirk leads a manhunt to a war-zone world to capture a one-man weapon of mass destruction.",  
     "title" : "Star Trek Into Darkness",  
     "score" : 7.968792915344238  
    }  
  
The document in the above results is a match because the `plot` contains the
terms `captain` and `kirk`, although only one is needed to meet the criteria
for a match, and the term `chess`, although not in the `plot`, appears in the
`fullplot`, which is the `defaultPath`.

← phraserange →

