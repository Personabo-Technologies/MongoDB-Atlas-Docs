Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# range

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Examples

## Definition

`range`

    

The `range` operator supports querying and scoring numeric and date values.
This operator can be used to perform a search over:

  * Number fields of BSON `int32`, `int64`, and `double` data types.

  * Date fields of BSON `date` data type in ISODate format.

You can use the `range` operator to find results that are within a given
numeric or date range.

## Syntax

`range` has the following syntax:

    
    
    1| {  
    |  
    2|     "$search": {  
    3|        "index": <index name>, // optional, defaults to "default"  
    4|        "range": {  
    5|           "path": "<field-to-search>",  
    6|           "gt | gte": <value-to-search>,  
    7|           "lt | lte": <value-to-search>,  
    8|           "score": <score-options>  
    9|        }  
    10|     }  
    11| }  
  
## Options

`range` uses the following terms to construct a query:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`gt` or `gte`

|

BSON date or number

|

Find values greater than (`>`) or greater than or equal to (`>=`) the given
value.

  * For number fields, the value can be an `int32`, `int64`, or `double` data type.

  * For date fields, the value must be an ISODate formatted date.

|

no  
  
`lt` or `lte`

|

BSON date or number

|

Find values less than (`<`) or less than or equal to (`<=`) the given value.

  * For number fields, the value can be an `int32`, `int64`, or `double` data type.

  * For date fields, the value must be an ISODate formatted date.

|

no  
  
`path`

|

string or array of strings

|

Indexed field or fields to search. See Path Construction.

|

yes  
  
`score`

|

object

|

Modify the score assigned to matching search results. Options are:

  * `boost`: multiply the result score by the given number.

  * `constant`: replace the result score with the given number.

For information on using `score` in your query, see Customize and Normalize
the Score in Results.

## Note

When querying values in arrays, Atlas Search doesn't alter the score based on
the number of values inside the array that matched the query. The score would
be the same as a single match irrespective of the number of matches inside an
array.

|

no  
  
## Examples

The following examples use the collection in the sample data. If you loaded
the sample data on your cluster, you can create the indexes using the index
definitions in the examples below and run the example queries on your cluster.

## Tip

If you've already loaded the sample dataset, follow the Get Started with Atlas
Search tutorial to create an index definition and run Atlas Search queries.

### Number Example

The following examples use indexes on numeric fields in the sample data and
run `range` queries against the indexed fields.

Example 1

Example 2

Example 3

The following example indexes and searches the numeric field `runtime` in the
`sample_mflix.movies collection`. The query uses `gte` and `lte` fields to
define the numeric range to search.

## Example

The following index definition named `default` indexes the `runtime` field in
the `movies` collection.

    
    
    {  
      
       "mappings": {  
          "dynamic": false,  
          "fields": {  
             "runtime": {  
                "type": "number"  
             }  
          }  
       }  
    }  
  
The following query searches for movies with a runtime greater than or equal
to `2` and less than equal to `3`. It includes a `$limit` stage to limit the
output to `5` results and a `$project` stage to exclude all fields except
`title` and `runtime`.

    
    
    1| db.movies.aggregate([  
    |  
    2|    {  
    3|       $search: {  
    4|          "range": {  
    5|             "path": "runtime",  
    6|             "gte": 2,  
    7|             "lte": 3  
    8|          }  
    9|       }  
    10|    },  
    11|    {  
    12|       $limit: 5  
    13|    },  
    14|    {  
    15|       $project: {  
    16|          "_id": 0,  
    17|          "title": 1,  
    18|          "runtime": 1  
    19|       }  
    20|    }  
    21| ])  
  
The above query returns the following search results:

    
    
    { "runtime" : 3, "title" : "Dots" }  
      
    { "runtime" : 3, "title" : "Sisyphus" }  
    { "runtime" : 3, "title" : "The Fly" }  
    { "runtime" : 2, "title" : "Andrè and Wally B." }  
    { "runtime" : 2, "title" : "Luxo Jr." }  
  
### Date Example

The following example uses the `range` operator to query a date field in the
`sample_mflix.movies` collection. For this example, you can use either static
or dynamic mappings to index the `date` type field named `released` in the
collection.

Dynamic Mapping Example

Static Mapping Example

The following index definition named `default` indexes all the dynamically
indexable fields in the `movies` collection, including the `released` field,
which is of type `date`.

    
    
    {  
      
       "mappings": {  
          "dynamic": true  
       }  
    }  
  
The following query searches for movies released between January 1, 2010 and
January 1, 2015. It includes a `$limit` stage to limit the output to 5 results
and a `$project` stage to exclude all fields except `title` and `released`.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "range": {  
    5|         "path": "released",  
    6|         "gt": ISODate("2010-01-01T00:00:00.000Z"),  
    7|         "lt": ISODate("2015-01-01T00:00:00.000Z")  
    8|       }  
    9|     }  
    10|   },  
    11|   {  
    12|     "$limit": 5  
    13|   },  
    14|   {  
    15|     "$project": {  
    16|       "_id": 0,  
    17|       "title": 1,  
    18|       "released": 1  
    19|     }  
    20|   }  
    21| ])  
  
The above query returns the following search results:

    
    
    1| { "title" : "The Fall of the House of Usher", "released" : ISODate("2011-09-20T00:00:00Z") }  
    |  
    2| { "title" : "The Blood of a Poet", "released" : ISODate("2010-05-20T00:00:00Z") }  
    3| { "title" : "Too Much Johnson", "released" : ISODate("2014-08-30T00:00:00Z") }  
    4| { "title" : "Stolen Desire", "released" : ISODate("2012-07-01T00:00:00Z") }  
    5| { "title" : "The Monkey King", "released" : ISODate("2012-01-12T00:00:00Z") }  
  
← queryStringregex →

