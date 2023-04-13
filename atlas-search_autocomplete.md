Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# autocomplete

Select your language

MongoDB Shell

On this page

  * Definition
  * Syntax
  * Options
  * Limitations
  * Examples
  * Index Definition
  * Basic Examples
  * Fuzzy Example
  * Token Order Example
  * Highlighting Example
  * Compound Example
  * Facet Example

## Definition

`autocomplete`

    

The autocomplete operator performs a search for a word or phrase that contains
a sequence of characters from an incomplete input string. You can use the
`autocomplete` operator with search-as-you-type applications to predict words
with increasing accuracy as characters are entered in your application's
search field. `autocomplete` returns results that contain predicted words
based on the tokenization strategy specified in the index definition for
autocompletion. The fields that you intend to query with the `autocomplete`
operator must be indexed with the How to Index Fields for Autocompletion data
type in the collection's index definition.

## Note

Atlas Search might return inaccurate results for queries with more than three
words in a single string.

## Syntax

`autocomplete` has the following syntax:

    
    
    1| {  
    |  
    2|   $search: {  
    3|     "index": "<index name>", // optional, defaults to "default"  
    4|     "autocomplete": {  
    5|       "query": "<search-string>",  
    6|       "path": "<field-to-search>",  
    7|       "tokenOrder": "any|sequential",  
    8|       "fuzzy": <options>,  
    9|       "score": <options>  
    10|     }  
    11|   }  
    12| }  
  
## Options

Field

|

Type

|

Description

|

Necessity

|

Default  
  
||||  
  
`query`

|

string or array of strings

|

String or strings to search for. If there are multiple terms in a string,
Atlas Search also looks for a match for each term in the string separately.

|

yes

|  
  
`path`

|

string

|

Indexed autocomplete type of field to search.

## Tip

### See also:

path construction

## Note

The `autocomplete` operator does not support `multi` in the field path.

|

yes

|  
  
`fuzzy`

|

object

|

Enable fuzzy search. Find strings which are similar to the search term or
terms.

|

no

|  
  
`fuzzy`

`.maxEdits`

|

integer

|

Maximum number of single-character edits required to match the specified
search term. Value can be `1` or `2`.

|

no

|

`2`  
  
`fuzzy`

`.prefixLength`

|

integer

|

Number of characters at the beginning of each term in the result that must
exactly match.

|

no

|

`0`  
  
`fuzzy`

`.maxExpansions`

|

integer

|

Maximum number of variations to generate and search for. This limit applies on
a per-token basis.

|

no

|

`50`  
  
`score`

|

object

|

score assigned to matching search term results. Use one of the following
options to modify the score:

|

|  
  
|  
  
`boost`

|

Multiply the result score by the given number.  
  
`constant`

|

Replace the result score with the given number.  
  
## Note

`autocomplete` offers less fidelity in score in exchange for faster query
execution.

no

|  
  
`tokenOrder`

|

string

|

Order in which to search for tokens. Value can be one of the following:

|

|  
  
|  
  
`any`

|

Indicates tokens in the query can appear in any order in the documents.
Results contain documents where the tokens appear sequentially and non-
sequentially. However, results where the tokens appear sequentially score
higher than other, non-sequential values.  
  
`sequential`

|

Indicates tokens in the query must appear adjacent to each other or in the
order specified in the query in the documents. Results contain only documents
where the tokens appear sequentially.  
  
no

|

`any`  
  
## Limitations

The `autocomplete` operator query results that are exact matches receive a
lower score than results that aren't exact matches. Atlas Search can't
determine if a query string is an exact match for an indexed text if you
specify just the autocomplete-indexed token substrings. To score exact matches
higher, try the following workaround:

## Note

The following workaround doesn't guarantee higher scores for exact matches in
all cases.

  1. Index the field as both How to Index Fields for Autocompletion and How to Index String Fields types.

Atlas Search `autocomplete` boosts exact matches when an `autocomplete` field
is also indexed as a `string`, thereby increasing the score of exact matches.

  2. Query using the compound operator.

For a demonstration of this workaround, see Compound Example.

## Examples

The following examples use the `movies` collection in the `sample_mflix`
database. If you loaded the sample dataset on your cluster, you can create the
static index for autocompletion and run the example queries on your cluster.

## Tip

If you've already loaded the sample dataset, follow the Get Started with Atlas
Search tutorial to create an index definition and run Atlas Search queries.

### Index Definition

The following tabs contain sample index definitions for the `edgeGram`,
`rightEdgeGram`, and `nGram` tokenization strategies.

edgeGram

rightEdgeGram

nGram

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "dynamic": false,  
    4|     "fields": {  
    5|       "title": [  
    6|         {  
    7|           "type": "stringFacet"  
    8|         },  
    9|         {  
    10|           "type": "string"  
    11|         },  
    12|         {  
    13|           "foldDiacritics": false,  
    14|           "maxGrams": 7,  
    15|           "minGrams": 3,  
    16|           "tokenization": "edgeGram",  
    17|           "type": "autocomplete"  
    18|         }  
    19|       ]  
    20|     }  
    21|   }  
    22| }  
  
MongoDB Shell

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
example on this page.

* * *

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

Run the following command at the `mongosh` prompt to use the `sample_mflix`
database:

    
    
    use sample_mflix  
      
  
MongoDB Shell

### Basic Examples

The following query searches for movies with the characters `off` in the
`title` field. The query includes a:

  * `$limit` stage to limit the output to 10 results.

  * `$project` stage to exclude all fields except `title`.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "autocomplete": {  
            "path": "title",  
            "query": "off"  
          }  
        }  
      },  
      {  
        $limit: 10  
      },  
      {  
        $project: {  
          "_id": 0,  
          "title": 1  
        }  
      }  
    ])  
  
MongoDB Shell

## Note

### Your Results May Vary

Atlas Search returns different results depending on the tokenization strategy
configured in the autocompletion field of the index definition. To learn more,
see Limitations.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

edgeGram

rightEdgeGram

nGram

    
    
    1| { title: 'Off Beat' },  
    |  
    2| { title: 'Off the Map' },  
    3| { title: 'Off and Running' },  
    4| { title: 'Hands off Mississippi' },  
    5| { title: 'Taking Off' },  
    6| { title: 'Noises Off...' },  
    7| { title: 'Brassed Off' },  
    8| { title: 'Face/Off' },  
    9| { title: 'Benji: Off the Leash!' },  
    10| { title: 'Set It Off' }  
  
MongoDB Shell

In the above results, the characters `off` appear at the left side of a word
in all the titles.

### Fuzzy Example

The following query searches for movies with the characters `pre` in the
`title` field. The query uses:

|  
  
|  
  
Field

|

Description  
  
`maxEdits`

|

Indicates that only one character variation is allowed in the query string
`pre` to match the query to a word in the documents.  
  
`prefixLength`

|

Indicates that the first character in the query string `pre` can't change when
matching the query to a word in the documents.  
  
`maxExpansions`

|

Indicates that up to two hundred and fifty six similar terms for `pre` can be
considered when matching the query string to a word in the documents.  
  
The query also includes a:

  * `$limit` stage to limit the output to 10 results.

  * `$project` stage to exclude all fields except `title`.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "autocomplete": {  
            "path": "title",  
            "query": "pre",  
            "fuzzy": {  
              "maxEdits": 1,  
              "prefixLength": 1,  
              "maxExpansions": 256  
            }  
          }  
        }  
      },  
      {  
        $limit: 10  
      },  
      {  
        $project: {  
          "_id": 0,  
          "title": 1  
        }  
      }  
    ])  
  
MongoDB Shell

## Note

### Your Results May Vary

Atlas Search returns different results depending on the tokenization strategy
configured in the autocompletion field of the index definition. To learn more,
see Limitations.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

edgeGram

rightEdgeGram

nGram

    
    
    1| { title: 'The Perils of Pauline' },  
    |  
    2| { title: 'The Blood of a Poet' },  
    3| { title: 'The Private Life of Henry VIII.' },  
    4| { title: 'The Private Life of Don Juan' },  
    5| { title: 'The Prisoner of Shark Island' },  
    6| { title: 'The Prince and the Pauper' },  
    7| { title: 'The Prisoner of Zenda' },  
    8| { title: 'Dance Program' },  
    9| { title: 'The Pied Piper' },  
    10| { title: 'Prelude to War' }  
  
MongoDB Shell

These results show the words that are predicted for the query string with one
character modification and with the first character constant at the left side
of the word in all the titles.

### Token Order Example

The following queries search for movies with the characters `men with` in the
`title` field. The queries also use the `tokenOrder` field, which specifies
whether the query searches for tokens in `any` order or in `sequential` order.

Each query includes a:

  * `$limit` stage to limit the output to 4 results.

  * `$project` stage to exclude all fields except `title`.

any

sequential

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "autocomplete": {  
          "path": "title",  
          "query": "men with",  
            "tokenOrder": "any"  
          }  
        }  
      },  
      {  
        $limit: 4  
      },  
      {  
        $project: {  
          "_id": 0,  
          "title": 1  
        }  
      }  
    ])  
  
MongoDB Shell

## Note

### Your Results May Vary

Atlas Search returns different results depending on the tokenization strategy
configured in the autocompletion field of the index definition. To learn more,
see Limitations.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

edgeGram

rightEdgeGram

nGram

    
    
    1| { title: 'Men with Guns' }  
    |  
    2| { title: 'Men with Brooms' }  
    3| { title: 'Men Without Women' }  
    4| { title: 'Brief Interviews with Hideous Men' }  
  
MongoDB Shell

### Highlighting Example

The following query searches for the characters `ger` in the `title` field of
the `movies` collection, with the `highlight` option enabled for the `title`
field.

The query includes a:

  * `$limit` stage to limit the output to 5 results.

  * `$project` stage to:

    * return the document's score.

    * exclude all fields except `title`.

    * add a new field called `highlights`, which contains highlighting information.

## Important

To highlight the autocomplete indexed version of a path, the autocomplete
operator must be the only operator that uses that path in the query.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "autocomplete": {  
            "path": "title",  
            "query": ["ger"]  
          },  
          "highlight": {   
            "path": "title"  
          }  
        }  
      },  
      {  
        $limit: 5  
      },   
      {   
        $project: {  
              
          "score": { $meta: "searchScore" },  
          "title": 1,  
          "_id": 0,  
          "highlights": { "$meta": "searchHighlights" }  
        }  
      }  
    ])  
  
MongoDB Shell

## Note

### Your Results May Vary

Atlas Search returns different results depending on the tokenization strategy
configured in the autocompletion field of the index definition. To learn more,
see Limitations.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

edgeGram

rightEdgeGram

nGram

    
    
    1| {  
    |  
    2|   title: 'Gertie the Dinosaur',  
    3|   score: 6.085907459259033,  
    4|   highlights: [{  
    5|     score: 0.9227690100669861,  
    6|     path: 'title',  
    7|     texts: [ { value: 'Gertie the Dinosaur', type: 'hit' } ]  
    8|   }]  
    9| },  
    10| {  
    11|   title: 'Germany Year Zero',  
    12|   score: 6.085907459259033,  
    13|   highlights: [{  
    14|     score: 0.9180012345314026,  
    15|     path: 'title',  
    16|     texts: [ { value: 'Germany Year Zero', type: 'hit' } ]  
    17|    }]  
    18| },  
    19| {  
    20|   title: 'Germany in Autumn',  
    21|   score: 6.085907459259033,  
    22|   highlights: [{  
    23|     score: 0.9180012345314026,  
    24|     path: 'title',  
    25|     texts: [ { value: 'Germany in Autumn', type: 'hit' } ]  
    26|   }]  
    27| },  
    28| {  
    29|   title: 'Germany Pale Mother',  
    30|   score: 6.085907459259033,  
    31|   highlights: [{  
    32|     score: 0.9227690100669861,  
    33|     path: 'title',  
    34|     texts: [ { value: 'Germany Pale Mother', type: 'hit' } ]  
    35|   }]  
    36| },  
    37| {  
    38|   title: 'Gerhard Richter - Painting',  
    39|   score: 6.085907459259033,  
    40|   highlights: [{  
    41|     score: 0.9386774897575378,  
    42|     path: 'title',  
    43|     texts: [ { value: 'Gerhard Richter - Painting', type: 'hit' } ]  
    44|   }]  
    45| }  
  
MongoDB Shell

Atlas Search returns these results because the characters `ger` appear at the
left side of a word in all the titles. Atlas Search matches a highlight `hit`
more coarsely to your query terms when a highlighted path is referenced only
in the autocomplete operators of the highlighted query.

### Compound Example

The following query searches for the characters `ball` in the `title` field of
the `movies` collection using the compound operator. The query specifies a
preference for documents that contain `ballroom` in the `title` field.

The query includes a:

  * `$limit` stage to limit the output to 10 results.

  * `$project` stage to:

    * return the document's score.

    * exclude all fields except `title`.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "compound": {  
    5|         "should": [{  
    6|           "autocomplete": {  
    7|             "path": "title",  
    8|             "query": "ball",  
    9|             "score": { "boost": { "value": 3}}  
    10|           }  
    11|         },  
    12|         {  
    13|           "text": {  
    14|             "path": "title",  
    15|             "query": "ball",  
    16|             "fuzzy": { "maxEdits": 1 }  
    17|           }  
    18|         }]  
    19|       }  
    20|     }  
    21|   },  
    22|   {  
    23|     $limit: 15  
    24|   },  
    25|   {  
    26|     $project: {  
    27|       "_id": 0,  
    28|       "title": 1,  
    29|       "score": { $meta: "searchScore" }  
    30|     }  
    31|   }  
    32| ])  
  
MongoDB Shell

## Note

### Your Results May Vary

Atlas Search returns different results depending on the tokenization strategy
configured in the autocompletion field of the index definition. To learn more,
see Limitations.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

edgeGram

rightEdgeGram

nGram

    
    
    1| [  
    |  
    2|   { title: 'Hard Ball', score: 28.687082290649414 },  
    3|   { title: 'The Ball', score: 28.687082290649414 },  
    4|   { title: "Monster's Ball", score: 28.687082290649414 },  
    5|   { title: 'Autumn Ball', score: 28.687082290649414 },  
    6|   { title: '8-Ball', score: 28.687082290649414 },  
    7|   { title: 'Operation Mad Ball', score: 26.25232696533203 },  
    8|   { title: 'The Ball at the Anjo House', score: 25.178993225097656 },  
    9|   { title: 'Dragon Ball Z: Battle of Gods', score: 25.178993225097656 },  
    10|   { title: 'Take Me Out to the Ball Game', score: 23.053739547729492 },  
    11|   { title: 'Fubar: Balls to the Wall', score: 19.069948196411133 },  
    12|   { title: 'Great Balls of Fire!', score: 18.041975021362305 },  
    13|   { title: 'Ballad of Narayama', score: 16.682058334350586 },  
    14|   { title: 'Ballad of a Soldier', score: 16.508026123046875 },  
    15|   { title: 'The Ballad of Narayama', score: 16.508026123046875 },  
    16|   { title: 'Ballistic: Ecks vs. Sever', score: 16.508026123046875 }  
    17| ]  
  
### Facet Example

The following query uses the `$searchMeta` stage to return unique values of
movies that contain the term `Gravity` in the `title` field of the `movies`
collection. The index definition of this query limits the results returned
from a How to Index String Fields For Faceted Search index, where both the
autocomplete and How to Index String Fields For Faceted Search types are on
the `title` field.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    1| db.movies.aggregate([{  
    |  
    2|   $searchMeta: {  
    3|     "facet": {  
    4|       "operator": {  
    5|         "autocomplete": {  
    6|           "query": "Gravity",  
    7|           "path": "title"  
    8|         }  
    9|       },  
    10|       "facets": {  
    11|         "titleFacet": {  
    12|           "type": "string",  
    13|           "path": "title"  
    14|         }  
    15|       }  
    16|     }  
    17|   }  
    18| }])  
  
MongoDB Shell

## Note

### Your Results May Vary

Atlas Search returns different results depending on the tokenization strategy
configured in the autocompletion field of the index definition. To learn more,
see Limitations.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    1| [{  
    |  
    2|    count: { lowerBound: Long("5") },  
    3|    facet: {  
    4|       titleFacet: {  
    5|       buckets: [  
    6|          { _id: 'Gravity', count: Long("3") },  
    7|          { _id: 'Defying Gravity', count: Long("1") },  
    8|          { _id: 'Laws of Gravity', count: Long("1") }  
    9|       ]  
    10|       }  
    11|    }  
    12| }]  
  
Atlas Search returns documents that contain the term `Gravity` in the `title`
field. The `count` field in the results indicate the number of documents in
the collection with the same title. In the results, Atlas Search found three
documents in the collection with `Gravity` as its title, but Atlas Search
ommited the duplicate titles and only returned one matching document.

If you want to see the duplicate titles as shown in the results below, run the
preceding autocomplete operator query using `$search` without facet.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    [  
      
      { title: 'Gravity' },  
      { title: 'Gravity' },  
      { title: 'Gravity' },  
      { title: 'Defying Gravity' },  
      { title: 'Laws of Gravity' }  
    ]  
  
MongoDB Shell

← Use Operators and Collectors in Atlas Search Queriescompound →

