Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# span

Share Feedback

On this page

  * Definition
  * Syntax
  * Examples
  * `first`
  * `near`
  * `or`
  * `subtract`

## Definition

`span`

    

The `span` operator finds text search matches within regions of a text field.
You can use it to find strings which are near each other to specified degrees
of precision. The `span` operator is more computationally intensive than other
operators, because queries must keep track of positional information.

`span` queries aren't ranked by score.

## Syntax

`span` has the following syntax:

    
    
    1| {  
    |  
    2|    $search: {  
    3|      "index": <index name>, // optional, defaults to "default"  
    4|      "span": {  
    5|        <clauses>: {  
    6|          <search queries>  
    7|        }  
    8|      }  
    9|    }  
    10| }  
  
## Note

`span` search queries can't use the compound operator.

## Examples

The examples on this page use a collection called `fruit` which contains the
following documents:

    
    
    1| {  
    |  
    2|   "_id" : 1,  
    3|   "type" : "apple",  
    4|   "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp."  
    5| },  
    6| {  
    7|   "_id" : 2,  
    8|   "type" : "banana",  
    9|   "description" : "Bananas are usually sold in bunches of five or six."  
    10| },  
    11| {  
    12|   "_id" : 3,  
    13|   "type" : "grapes",  
    14|   "description" : "Six bunches of grapes weigh about 3 pounds."  
    15| }  
  
### `first`

The following example uses a `first` clause to find documents in which the
string `bunches` appears near the beginning of the `description` field. The
`endPositionLte` parameter has a value of `2`, specifying that the search term
must be the first or second word in the field.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "span": {  
    5|         "first": {  
    6|           "operator": {  
    7|             "term": {  
    8|               "path": "description",  
    9|               "query": "bunches"  
    10|             }  
    11|           },  
    12|           "endPositionLte": 2  
    13|         }  
    14|       }  
    15|     }  
    16|   }  
    17| ])  
  
The above query returns the document with `_id: 3`, which has a `description`
field with `bunches` as the second word.

    
    
    {  
      
      "_id": 3,  
      "type": "grapes",  
      "description": "Six bunches of grapes weigh about 3 pounds."  
    }  
  
### `near`

The following query looks for documents in which the strings `bunches` and
`bananas` are found near each other. The `inOrder` parameter is set to
`false`, so the search terms can be in any order. The `slop` parameter is set
to `4`, so the search terms must be separated by no more than 4 words.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search : {  
    4|       "span": {  
    5|         "near": {  
    6|           "clauses": [  
    7|             { "term": { "path": "description", "query": "bunches" } },  
    8|             { "term": { "path": "description", "query": "bananas" } }  
    9|           ],  
    10|           "slop": 4,  
    11|           "inOrder": false  
    12|         }  
    13|       }  
    14|     }  
    15|   }  
    16| ])  
  
The above query finds the following result:

    
    
    {  
      
     "_id": 2,  
     "type": "banana",  
     "description": "Bananas are usually sold in bunches of five or six."  
    }  
  
### `or`

The following query uses two `term` clauses to look for documents in which the
`description` field has either `bananas` or `apples` as the first word.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "span": {  
    5|         "first": {  
    6|           "endPositionLte": 1,  
    7|           "operator": {  
    8|             "or": {  
    9|               "clauses": [  
    10|                 { "term": { "path": "description", "query": "bananas" } },  
    11|                 { "term": { "path": "description", "query": "apples" } }  
    12|               ]  
    13|             }  
    14|           }  
    15|         }  
    16|       }  
    17|     }  
    18|   }  
    19| ])  
  
The above query finds the following results:

    
    
    {  
      
      "_id": 1,  
      "type": "apple",  
      "description": "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp."  
    }, {  
      "_id": 2,  
      "type": "banana",  
      "description": "Bananas are usually sold in bunches of five or six."  
    }  
  
### `subtract`

The `subtract` clause is useful for excluding certain strings from your search
results. The following query looks for documents in which the `description`
field contains the words `six` and `bunches`, in any order, within 3 words of
each other. It excludes any document in which the word `five` occurs between
`six` and `bunches`.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search : {  
    4|       "span": {  
    5|         "subtract": {  
    6|           "include": {  
    7|             "near": {  
    8|               "clauses": [  
    9|                 { "term": { "path": "description", "query": "six" } },  
    10|                 { "term": { "path": "description", "query": "bunches" } }  
    11|               ],  
    12|               "inOrder": false,  
    13|               "slop": 3  
    14|             }  
    15|           },  
    16|           "exclude": { "term": { "path": "description", "query": "five" } }  
    17|         }  
    18|       }  
    19|     }  
    20|   }  
    21| ])  
  
The above query finds the following result:

    
    
    {  
      
     "_id": 3,  
     "type": "grapes",  
     "description": "Six bunches of grapes weigh about 3 pounds."  
    }  
  
The document with `_id: 2` isn't included. Although its `description` field
includes the words `six` and `bunches`, it also has `five` between them, and
`five` is in the `exclude` clause of the query.

← regextext →

