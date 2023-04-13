Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# phrase

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Examples
  * Single Phrase Example
  * Multiple Phrases Example
  * Slop Example

## Definition

`phrase`

    

The `phrase` operator performs search for documents containing an ordered
sequence of terms using the analyzer specified in the index configuration. If
no analyzer is specified, the default standard analyzer is used.

## Syntax

`phrase` has the following syntax:

    
    
    1| {  
    |  
    2|   $search: {  
    3|      "index": <index name>, // optional, defaults to "default"  
    4|      "phrase": {  
    5|        "query": "<search-string>",  
    6|        "path": "<field-to-search>",  
    7|        "score": <options>,  
    8|        "slop": <distance-number>  
    9|      }  
    10|   }  
    11| }  
  
## Options

`phrase` uses the following terms to construct a query:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`query`

|

string or array of strings

|

String or strings to search for.

|

yes  
  
`path`

|

string or array of strings

|

Indexed field or fields to search. You can also specify a wildcard path to
search. See path construction.

|

yes  
  
`slop`

|

integer

|

Allowable distance between words in the `query` phrase. Lower value allows
less positional distance between the words and greater value allows more
reorganization of the words and more distance between the words to satisfy the
query. The default is `0`, meaning that words must be exactly in the same
position as the query in order to be considered a match. Exact matches are
scored higher.

|

no  
  
`score`

|

object

|

Score assigned to matching search results. You can modify the score using the
following options:

  * `boost`: multiply the result score by the given number.

  * `constant`: replace the result score with the given number.

|

no  
  
## Examples

The following examples use the `movies` collection in the `sample_mflix`
database. If you have the sample dataset on your cluster, you can create the
index on the `title` field and run the example queries on your cluster.

## Tip

If you've already loaded the sample dataset, follow the Get Started with Atlas
Search tutorial to create an index definition and run Atlas Search queries.

### Single Phrase Example

The following Atlas Search example performs a basic search of the `title`
field for the query string `new york`. There is no `slop` in the query and so
the `slop` value defaults to `0`, which means the position of the words must
exactly match the query string to be included in the results. The query also
includes a:

  * `$limit` stage to limit the output to 10 results.

  * `$project` stage to exclude all fields except `title` and add a field named `score`.

## Example

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "phrase": {  
    5|         "path": "title",  
    6|         "query": "new york"  
    7|       }  
    8|     }  
    9|   },  
    10|   { $limit: 10 },  
    11|   {  
    12|     $project: {  
    13|       "_id": 0,  
    14|       "title": 1,  
    15|       score: { $meta: "searchScore" }  
    16|     }  
    17|   }  
    18| ])  
  
The above query returns the following results:

    
    
    1| { "title" : "New York, New York", "score" : 6.75715970993042 }  
    |  
    2| { "title" : "New York", "score" : 6.231321334838867 }  
    3| { "title" : "New York Stories", "score" : 5.358973026275635 }  
    4| { "title" : "New York Minute", "score" : 5.358973026275635 }  
    5| { "title" : "Synecdoche, New York", "score" : 5.358973026275635 }  
    6| { "title" : "New York Doll", "score" : 5.358973026275635 }  
    7| { "title" : "Little New York", "score" : 5.358973026275635 }  
    8| { "title" : "Escape from New York", "score" : 4.700878143310547 }  
    9| { "title" : "King of New York", "score" : 4.700878143310547 }  
    10| { "title" : "Naked in New York", "score" : 4.700878143310547 }  
  
### Multiple Phrases Example

The following Atlas Search example performs a basic search of the `title`
field for the query strings `the man` and `the moon`. There is no `slop` in
the query and so the `slop` value defaults to `0`, which means the position of
the words must exactly match the query string to be included in the results.
The query also includes a:

## Example

  * `$limit` stage to limit the output to 10.

  * `$project` stage to exclude all fields except `title` and add a field named `score`.

    
    
    1| db.movies.aggregate([  
    |  
    2| {  
    3|   "$search": {  
    4|     "phrase": {  
    5|       "path": "title",  
    6|       "query": ["the man", "the moon"]  
    7|     }  
    8|   }  
    9| },  
    10| { $limit: 10 },  
    11| {  
    12|   $project: {  
    13|     "_id": 0,  
    14|     "title": 1,  
    15|     score: { $meta: "searchScore" }  
    16|   }  
    17| }  
    18| ])  
  
The above query returns the following results:

    
    
    1| { "title" : "The Man in the Moon", "score" : 4.500046730041504 }  
    |  
    2| { "title" : "Shoot the Moon", "score" : 3.278003215789795 }  
    3| { "title" : "Kick the Moon", "score" : 3.278003215789795 }  
    4| { "title" : "The Man", "score" : 2.8860299587249756 }  
    5| { "title" : "The Moon and Sixpence", "score" : 2.8754563331604004 }  
    6| { "title" : "The Moon Is Blue", "score" : 2.8754563331604004 }  
    7| { "title" : "Racing with the Moon", "score" : 2.8754563331604004 }  
    8| { "title" : "Mountains of the Moon", "score" : 2.8754563331604004 }  
    9| { "title" : "Man on the Moon", "score" : 2.8754563331604004 }  
    10| { "title" : "Castaway on the Moon", "score" : 2.8754563331604004 }  
  
### Slop Example

The following Atlas Search example performs a search of the `title` field for
the query string `men women`. The `slop` value of `5` in the `query` allows
greater movement of the words and distance between the words `men` and
`women`. The query includes a `$project` stage to:

  * Exclude all fields except `title`

  * Add a field named `score`

## Example

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "phrase": {  
    5|         "path": "title",  
    6|         "query": "men women",  
    7|         "slop": 5  
    8|       }  
    9|     }  
    10|   },  
    11|   {  
    12|     $project: {  
    13|       "_id": 0,  
    14|       "title": 1,  
    15|       score: { $meta: "searchScore" }  
    16|     }  
    17|   }  
    18| ])  
  
The above query returns the following results:

    
    
    { "title" : "Men Without Women", "score" : 3.39743709564209 }  
      
    { "title" : "Men Vs Women", "score" : 3.39743709564209 }  
    { "title" : "Good Men, Good Women", "score" : 2.878715753555298 }  
    { "title" : "The War Between Men and Women", "score" : 2.205303192138672 }  
    { "title" : "Women Without Men", "score" : 1.983487844467163 }  
    { "title" : "Women Vs Men", "score" : 1.983487844467163 }  
  
← nearqueryString →

