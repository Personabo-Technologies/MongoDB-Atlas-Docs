Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# exists

Share Feedback

On this page

  * Definition
  * Syntax
  * Examples

## Definition

`exists`

    

The `exists` operator tests if a path to a specified indexed field name exists
in a document. If the specified field exists but is not indexed, the document
is not included with the result set. `exists` is often used as part of a
compound query in conjunction with other search clauses.

## Syntax

`exists` has the following syntax:

    
    
    1| {  
    |  
    2|   $search: {  
    3|     "index": <index name>, // optional, defaults to "default"  
    4|     "exists": {  
    5|       "path": "<field-to-test-for>",  
    6|     }  
    7|   }  
    8| }  
  
## Examples

The examples on this page use a collection called `fruit` that contains the
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
    11| { "_id" : 3,  
    12|   "type": "apple",  
    13|   "description" : "Apple pie and apple cobbler are popular apple-based desserts."  
    14| },  
    15| { "_id" : 4,  
    16|   "description" : "Types of citrus fruit include lemons, oranges, and grapefruit.",  
    17|   "quantities" : {  
    18|     "lemons": 200,  
    19|     "oranges": 240,  
    20|     "grapefruit": 160  
    21|   }  
    22| }  
  
The `fruit` collection has an Atlas Search index on the `description` field
that uses the standard analyzer. The `standard` analyzer lower-cases all words
and disregards common stop words (`"the", "a", "and",` etc).

### Basic Example

The following example searches for documents which include a field called
`type`:

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "exists": {  
    5|         "path": "type"  
    6|       }  
    7|     }  
    8|   }  
    9| ])  
  
The above query returns the first three documents of the collection. The
document with `_id: 4` is not included because it does not have a `type`
field.

### Embedded Example

Use dot notation to search for embedded fields. The following example searches
for documents which have a field named `lemons` embedded within a field named
`quantities`.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "exists": {  
    5|         "path": "quantities.lemons"  
    6|       }  
    7|     }  
    8|   }  
    9| ])  
  
The above query returns the following result:

    
    
    1| {  
    |  
    2|   "_id" : 4,  
    3|   "description" : "Types of citrus fruit include lemons, oranges, and grapefruit.",  
    4|   "quantities" : {  
    5|     "lemons": 200,  
    6|     "oranges": 240,  
    7|     "grapefruit": 160  
    8|   }  
    9| }  
  
### Compound Example

The following example uses `exists` as part of a compound query.

    
    
    1| db.fruit.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "compound": {  
    5|         "must": [  
    6|           {  
    7|             "exists": {  
    8|               "path": "type"  
    9|             }  
    10|           },  
    11|           {  
    12|             "text": {  
    13|               "query": "apple",  
    14|               "path": "type"  
    15|             }  
    16|           }],  
    17|         "should": {  
    18|           "text": {  
    19|             "query": "fuji",  
    20|             "path": "description"  
    21|           }  
    22|         }  
    23|       }  
    24|     }  
    25|   }  
    26| ])  
  
The above query returns the following results:

    
    
    1| {  
    |  
    2|   "_id" : 1,  
    3|   "type" : "apple",  
    4|   "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp."  
    5| }  
    6| {  
    7|   "_id" : 3,  
    8|   "type" : "apple",  
    9|   "description" : "Apple pie and apple cobbler are popular apple-based desserts."  
    10| }  
  
Both documents have a `type` field, and both include the search term `apple`.
The document with `_id: 1` is returned first because it satisfies the `should`
clause.

← equalsfacet →

