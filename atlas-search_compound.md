Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# compound

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Usage
  * Examples

## Definition

`compound`

    

The `compound` operator combines two or more operators into a single query.
Each element of a `compound` query is called a clause, and each clause
consists of one or more sub-queries.

Documents in the result set are returned with a match score, which is
calculated by summing the score that each document received for each
individual clause which generated a match. The result set is ordered by score,
highest to lowest.

## Syntax

`compound` has the following syntax:

    
    
    1| {  
    |  
    2|   $search: {  
    3|     "index": <index name>, // optional, defaults to "default"  
    4|     "compound": {  
    5|       <must | mustNot | should | filter>: [ { <clauses> } ],  
    6|       "score": <options>  
    7|     }  
    8|   }  
    9| }  
  
Each `must`, `mustNot`, `should`, and `filter` clause contains an array of
subclauses. Use array syntax even if the array contains only one subclause.
See the examples on this page.

## Options

`compound` uses the following terms to construct a query:

|  
  
|  
  
`must`

    

|

Clauses that must match to for a document to be included in the results. The
returned score is the sum of the scores of all the subqueries in the clause.

Maps to the `AND` boolean operator.  
  
`mustNot`

    

|

Clauses that must not match for a document to be included in the results.
`mustNot` clauses don't contribute to a returned document's score.

Maps to the `AND NOT` boolean operator.  
  
`should`

    

|

Clauses that you prefer to match in documents that are included in the
results. Documents that contain a match for a `should` clause have higher
scores than documents that don't contain a `should` clause. The returned score
is the sum of the scores of all the subqueries in the clause.

If you use more than one `should` clause, you can use the `minimumShouldMatch`
option to specify a minimum number of `should` clauses that must match to
include a document in the results. If omitted, the `minimumShouldMatch` option
defaults to `0`.

See an example.

Maps to the `OR` boolean operator.  
  
`filter`

    

|

Clauses that must all match for a document to be included in the results.
`filter` clauses do not contribute to a returned document's score.

## Example

For example, you can replace the `$match` stage with the `compound` operator
`filter` condition in the `$search` stage:

    
    
    | {  
      
      "$match": {  
        "role": { "$in": [ "CLIENT", "PROFESSIONAL" ] }  
      }  
    }  
  
You can use the `filter` option instead:

    
    
    $search: {  
      
      "compound": {  
        "filter": [{  
          "text": {  
            "query": ["CLIENT", "PROFESSIONAL"],  
            "path": "role"  
          }  
        }]  
      }  
    }  
  
See another filter example.  
  
`score`

|

Modify the score of the entire `compound` clause. You can use `score` to
boost, replace, or otherwise alter the score. If you don't specify `score`,
the returned score is the sum of the scores of all the subqueries in the
`must` and `should` clauses that generated a match.  
  
## Usage

You can use any of the clauses with any top-level operator, such as
autocomplete, text, or span, to specify query criteria.

You can boost or replace the score of the entire compound query. For an
example of replacing the entire compound score, see Compound Score Example
below. You can use score to also boost or alter the score for each subquery in
each clause. For some examples of altered scores in `compound` operator
clauses, see Customize and Normalize the Score in Results.

## Examples

The examples on this page use a collection called `fruit`, which contains the
following documents:

    
    
    1| {  
    |  
    2|   "_id" : 1,  
    3|   "type" : "apple",  
    4|   "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp.",  
    5|   "category" : "nonorganic",  
    6|   "in_stock" : false  
    7| },  
    8| {  
    9|   "_id" : 2,  
    10|   "type" : "banana",  
    11|   "description" : "Bananas are usually sold in bunches of five or six.",  
    12|   "category" : "nonorganic",  
    13|   "in_stock" : true  
    14| },  
    15| {  
    16|   "_id" : 3,  
    17|   "type" : "pear",  
    18|   "description" : "Bosc and Bartlett are the most common varieties of pears.",  
    19|   "category" : "organic",  
    20|   "in_stock" : true  
    21| }  
  
The `fruit` collection has an Atlas Search index on the `description` field
which uses the standard analyzer. The `standard` analyzer lower-cases all
words and disregards common stop words (`"the", "a", "and",` etc).

### `must` and `mustNot` Example

The following example uses a combination of `must` and `mustNot` clauses to
contruct a query. The `must` clause uses the text operator to search for the
term `varieties` in the `description` field. For a document to match, it must
fulfill the `must` clause. The `mustNot` clause performs a search operation
for the term `apples` in the `description` field. For a document to match, it
must _not_ fulfill the `mustNot` clause.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "compound": {  
    5|         "must": [{  
    6|           "text": {  
    7|             "query": "varieties",  
    8|             "path": "description"  
    9|           }  
    10|         }],  
    11|         "mustNot": [{  
    12|           "text": {  
    13|             "query": "apples",  
    14|             "path": "description"  
    15|           }  
    16|         }]  
    17|       }  
    18|     }  
    19|   }  
    20| ])  
  
The above query returns the document with `_id: 3` because its `description`
field contains the word `varieties` and does not contain `apples`.

### `must` and `should` Example

The following queries use `must` to specify search conditions that must be met
and `should` to specify preference for documents that contain the word `Fuji`.

Basic Example

Compound Score Example

For this query, the `$project` pipeline stage excludes all document fields
except `_id` and adds a `score` field, which displays the document's relevance
score.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "compound": {  
    5|         "must": [{  
    6|           "text": {  
    7|             "query": "varieties",  
    8|             "path": "description"  
    9|           }  
    10|         }],  
    11|         "should": [{  
    12|           "text": {  
    13|             "query": "Fuji",  
    14|             "path": "description"  
    15|           }  
    16|         }]  
    17|       }  
    18|     }  
    19|   },  
    20|   {  
    21|     "$project": {  
    22|       "score": { "$meta": "searchScore" }  
    23|     }  
    24|   }  
    25| ])  
  
The above query returns the following results:

    
    
    { "_id" : 1, "score" : 0.6425117254257202 }  
      
    { "_id" : 3, "score" : 0.21649497747421265 }  
  
The document with `_id: 1` has a higher score because its `description` field
contains the word `Fuji`, satisfying the `should` clause.

### minimumShouldMatch Example

In a query with multiple `should` clauses, you can use the
`miniumumShouldMatch` option to specify a minimum number of clauses which must
match to return a result.

The following query has one `must` clause and two `should` clauses, with a
`minimumShouldMatch` value of `1`. A document must include the term
`varieties` in the `description` field and must include either `Fuji` or
`Golden Delicious` in the description field to be included in the result set.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "compound": {  
    5|         "must": [{  
    6|           "text": {  
    7|              "query": "varieties",  
    8|              "path": "description"  
    9|           }  
    10|         }],  
    11|         "should": [  
    12|           {  
    13|             "text": {  
    14|               "query": "Fuji",  
    15|               "path": "description"  
    16|             }  
    17|           },  
    18|           {  
    19|             "text": {  
    20|               "query": "Golden Delicious",  
    21|               "path": "description"  
    22|             }  
    23|           }],  
    24|           "minimumShouldMatch": 1  
    25|         }  
    26|       }  
    27|     }  
    28| ])  
  
The above query returns the following result:

    
    
    {  
      
      "_id" : 1,  
      "type" : "apple",  
      "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp.",  
      "category" : "nonorganic",  
      "in_stock" : false  
    }  
  
The document with `_id: 1` matches the `must` clause and the first of the two
`should` clauses.

### `filter` Examples

`filter` behaves the same as `must`, except that the `filter` clause is not
considered in a returned document's score, and therefore does not affect the
order of the returned documents.

Basic Example

$match Replacement Example

The following query uses the following clauses:

  * `must` and `filter` to specify search conditions which must be met.

  * `should` to specify preference for documents containing the word `banana`. The `should` clause doesn't include the `minimumShouldMatch` option. When you omit `minimumShouldMatch`, it defaults to `0`.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "compound": {  
    5|         "must": [{  
    6|           "text": {  
    7|             "query": "varieties",  
    8|             "path": "description"  
    9|           }  
    10|         }],  
    11|         "should": [{  
    12|           "text": {  
    13|             "query": "banana",  
    14|             "path": "description"  
    15|           }  
    16|         }],  
    17|         "filter": [{  
    18|           "text": {  
    19|             "query": "granny",  
    20|             "path": "description"  
    21|           }  
    22|         }]  
    23|       }  
    24|     }  
    25|   }  
    26| ])  
  
The query returns the following result:

    
    
    {  
      
      "_id" : 1,  
      "type" : "apple",  
      "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp.",  
      "category" : "nonorganic",  
      "in_stock" : false  
    }  
  
The returned document fulfills all the requirements for inclusion:

  * Both the `must` clause and the `filter` clause match.

  * The `minimumShouldMatch` value is not specified, so it defaults to `0`. As a result, the `should` clause fails and still returns a document.

### Nested Example

The following example uses nested `compound` clauses to construct a query. For
this example, the `fruit` collection has an index on the `type`, `category`,
and `in_stock` fields, whose text fields use the default analyzer. The query
requires documents to only satisfy one of the following `should` clauses:

  * Contain the word `apple` in the `type` field.

  * Contain the term `organic` in the `category` field and have the value `true` in the `in_stock` field.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "compound": {  
    5|         "should": [  
    6|           {  
    7|             "text": {  
    8|               "query": "apple",  
    9|               "path": "type"  
    10|             }  
    11|           },  
    12|           {  
    13|             "compound": {  
    14|               "must": [  
    15|                 {  
    16|                   "text": {  
    17|                     "query": "organic",  
    18|                     "path": "category"  
    19|                   }  
    20|                 },  
    21|                 {  
    22|                   "equals": {  
    23|                     "value": true,  
    24|                     "path": "in_stock"  
    25|                   }  
    26|                 }  
    27|               ]  
    28|             }  
    29|           }  
    30|         ],  
    31|         "minimumShouldMatch": 1  
    32|       }  
    33|     }  
    34|   }  
    35| ])  
  
The above query returns the following result:

    
    
    {  
      
      "_id" : 3,  
      "type" : "pear",  
      "description" : "Bosc and Bartlett are the most common varieties of pears.",  
      "category" : "organic",  
      "in_stock" : true  
    }  
    {  
      "_id" : 1,  
      "type" : "apple",  
      "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp.",  
      "category" : "nonorganic",  
      "in_stock" : false  
    }  
  
The above document fulfills all the requirements for inclusion:

  * The document with `_id: 3` matches the `must` clause nested within the second `should` clause.

  * The document with `_id: 1` matches the first `should` clause.

← autocompleteembeddedDocument →

