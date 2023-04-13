Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Sort Atlas Search Results

Share Feedback

On this page

  * Overview
  * Usage
  * Considerations
  * Limitations
  * Index Definition
  * Sort by Date
  * Sort by Number
  * Sort by String
  * `sortBetaV1` Operator
  * Syntax
  * Behavior
  * Examples

## Important

This feature is in Beta. Make a note of the following:

  * The name and syntax of the field types and operator might change during Beta and will change for GA.

  * Resource usage might change. For more information, see Considerations.

## Overview

Atlas Search supports sorting in ascending or descending order on fields that
you define in your Atlas Search index for sorting. You can sort by date,
number (integer, float, and double values), and string values using the
`sortBetaV1` operator.

### Usage

To sort your Atlas Search results, you must do the following:

  1. Create an Atlas Search index on the fields your wish to sort your results by. To learn more, see Index Definition.

  2. Create and run your query using the `sortBetaV1` operator against the fields you defined in the index for sorting. To learn more, see `sortBetaV1` Operator.

### Considerations

#### Consistency

Atlas Search indexes are eventually consistent, and values returned in results
might be different from values used in sorting.

#### Performance

This feature optimizes queries that use `$search` with `$limit` as a
subsequent stage. If Atlas Search needs to sort all documents in the
collection, the response might be slow.

#### Scoring

Atlas Search returns scores for all documents in the results.

### Limitations

The following limitations apply:

  * You can't index and sort on fields in sharded collections.

  * You can't sort and facet in the same query.

  * You can't sort on fields in How to Index Fields in Arrays of Objects and Documents.

  * You can't configure a field with more than one of `sortableDateBetaV1`, `sortableNumberBetaV1`, or `sortableStringBetaV1` field types.

## Index Definition

To sort by date, number, or string values, you must index these fields as a
`sortableDateBetaV1`, `sortableNumberBetaV1`, or `sortableStringBetaV1` type
respectively.

## Note

When you index a field as `sortableDateBetaV1`, `sortableNumberBetaV1`, or
`sortableStringBetaV1` type, you can only _sort_ your results by that field.
To also _query_ that field, you must index that field as also `date`,
`number`, or `string` type.

### Sort by Date

Use `sortableDateBetaV1` type to index date fields for sorting.

#### Option

The `sortableDateBetaV1` type has the following option:

Option

|

Type

|

Necessity

|

Purpose  
  
|||  
  
`type`

|

string

|

Required

|

Human-readable label that identifies this field type. Value must be
`sortableDateBetaV1`.  
  
#### Example

The following index definition for the `sample_mflix.movies` collection in the
sample dataset indexes the date field `released` for sorting.

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "released": {  
            "type": "sortableDateBetaV1"  
          }  
        }  
      }  
    }  
  
### Sort by Number

Use `sortableNumberBetaV1` type to index numeric fields for sorting.

## Note

Atlas Search converts `int32` and `int64` values to `double` when indexing the
field, which might result in loss of precision for `int64` values larger than
`2^53` and smaller than `-2^53`.

#### Option

The `sortableNumberBetaV1` type has the following option:

Option

|

Type

|

Necessity

|

Purpose  
  
|||  
  
`type`

|

string

|

Required

|

Human-readable label that identifies this field type. Value must be
`sortableNumberBetaV1`.  
  
#### Example

The following index definition for the `sample_mflix.movies` collection in the
sample dataset indexes the numeric field `awards.wins` for sorting.

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "awards": {  
            "type": "document",  
            "dynamic": false,  
            "fields": {  
              "wins": {  
                "type": "sortableNumberBetaV1"  
              }  
            }  
          }  
        }  
      }  
    }  
  
### Sort by String

Use `sortableStringBetaV1` type to index string fields for sorting.

#### Option

The `sortableStringBetaV1` type has the following option:

Option

|

Type

|

Necessity

|

Purpose  
  
|||  
  
`type`

|

string

|

Required

|

Human-readable label that identifies this field type. Value must be
`sortableStringBetaV1`.  
  
#### Example

The following index definition for the `sample_mflix.movies` collection in the
sample dataset indexes the string field `title` for sorting.

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "title": {  
            "type": "sortableStringBetaV1"  
          }  
        }  
      }  
    }  
  
## `sortBetaV1` Operator

`sortBetaV1`

    

The `sortBetaV1` operator sorts your Atlas Search results in ascending or
descending order based on the fields you defined in your Atlas Search index
for sorting.

### Syntax

`sortBetaV1` operator has the following syntax:

    
    
    {  
      
      "sortBetaV1": {  
        "<field-name-to-sort-by>": <sort-order>,  
        ...  
      }  
    }  
  
### Behavior

The `sortBetaV1` takes a document that specifies the fields to sort by and the
respective sort order.

You can specify the following sort order to sort your results by:

|  
  
|  
  
`1`

|

Sort in ascending order.

When you sort in ascending order, Atlas Search returns documents with missing
values before documents with values.  
  
`-1`

|

Sort in descending order .  
  
Atlas Search flattens the arrays for sorting.

## Example

Consider the following array:

    
    
    [4, [1, [8,5], 9], 2]  
      
  
Atlas Search flattens the preceding array similar to the following:

    
    
    4, 1, 8, 5, 9, 2  
      
  
For an ascending sort, Atlas Search uses `1` to compare the array to other
values. For a descending sort, Atlas Search uses `9` to compare the array to
other values.

When comparing with elements inside an array:

  * For an ascending sort, Atlas Search compares the smallest elements of the array or performs a less than (`<`) comparison.

## Example

Atlas Search sorts results in the following order if you sort by numbers in
ascending order:

    
        -20  
      
    [-3, 12] // <- -3 comes before 5.  
    5  
    [6, 18]  // <- 6 comes after 5.  
    13  
    14  
  
  * For a descending sort, Atlas Search compares the largest elements of the array or performs a greater than (`>`) comparison.

## Example

Atlas Search sorts results in the following order if you sort by numbers in
descending order:

    
        [6, 18]  // <- 18 comes before 14.  
      
    14  
    13  
    [-3, 12] // <- 12 comes after 13.  
    5  
    -20  
  

### Examples

The following examples use the `sample_mflix.movies` collection in the sample
data.

#### Index Definition

The example queries in this section use the following index. The index
definition for the collection specifies the following:

  * Index `awards.wins` field as `sortableNumberBetaV1` type for sorting and `number` type for querying.

  * Index `released` field as `sortableDateBetaV1` type for sorting and `date` type for querying.

  * Index `title` field as `sortableStringBetaV1` type for sorting and `string` type for querying.

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "awards": {  
            "dynamic": false,  
            "fields": {  
              "wins": [  
                {  
                  "type": "sortableNumberBetaV1"  
                },  
                {  
                  "type": "number"  
                }  
              ]  
            },  
            "type": "document"  
          },  
          "released": [{  
            "type": "sortableDateBetaV1"  
          }, {  
            "type": "date"  
          }],  
          "title": [{  
            "type": "sortableStringBetaV1"  
          }, {  
            "type": "string"  
          }]  
        }  
      }  
    }  
  
For the preceding index definition, Atlas Search creates an index named
`default` with static mappings on the specified fields.

#### Date Search and Sort

The following query uses the `$search` stage to do the following:

  * Search for movies released between 01 January, 2010 and 01, January, 2015 using the range operator.

  * Sort the results in descending order of released date using `sortBetaV1` operator.

The query uses the `$limit` stage to limit the output to `5` documents. It
also uses the `$project` stage to omit all fields except `title` and
`released` in the results.

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "range": {  
            "path": "released",  
            "gt": ISODate("2010-01-01T00:00:00.000Z"),  
            "lt": ISODate("2015-01-01T00:00:00.000Z")  
          },  
          "sortBetaV1": {  
            "released": -1  
          }  
        }  
      },  
      {  
        "$limit": 5  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1,  
          "released": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        title: 'Cold in July',  
        released: ISODate("2014-12-31T00:00:00.000Z")  
      },  
      {  
        title: 'The Gambler',  
        released: ISODate("2014-12-31T00:00:00.000Z")  
      },  
      {  
        title: 'Force Majeure',  
        released: ISODate("2014-12-30T00:00:00.000Z")  
      },  
      {  
        title: 'LFO',  
        released: ISODate("2014-12-27T00:00:00.000Z")  
      },  
      {  
        title: 'Peace After Marriage',  
        released: ISODate("2014-12-26T00:00:00.000Z")  
      }  
    ]  
  
#### Number Search and Sort

The following query uses the `$search` stage to do the following:

  * Search for movies that have won awards.

  * Sort the results in descending order using `sortBetaV1` operator.

The query uses the `$limit` stage to limit the output to `5` documents. It
also uses the `$project` stage to omit all fields except `title` and
`awards.wins` in the results.

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
           "range": {  
             "path": "awards.wins",  
             "gt": 3  
          },  
          "sortBetaV1": {  
            "awards.wins": -1  
          }  
        }  
      },  
      {  
        "$limit": 5  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1,  
          "awards.wins": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      { title: '12 Years a Slave', awards: { wins: 267 } },  
      { title: 'Gravity', awards: { wins: 231 } },  
      { title: 'Gravity', awards: { wins: 231 } },  
      {  
        title: 'Birdman: Or (The Unexpected Virtue of Ignorance)',  
        awards: { wins: 210 }  
      },  
      { title: 'Boyhood', awards: { wins: 185 } },  
    ]  
  
#### String Search and Sort

The following query uses the `$search` stage to do the following:

  * Search for movies that have the term `country` in the title.

  * Sort the results in ascending order using `sortBetaV1` operator.

The query uses the `$limit` stage to limit the output to `5` documents. It
also uses the `$project` stage to do the following:

  * Omit all fields except `title` in the results.

  * Add a field named `score`.

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "text": {  
            "path": "title",  
            "query": "country"  
          },  
          "sortBetaV1": {  
            "title": 1  
          }  
        }  
      },  
      {  
        "$limit": 5  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1,  
          "score": { "$meta": "searchScore" }  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      { title: 'A Country Called Home', score: 2.5108444690704346 },  
      { title: 'A Day in the Country', score: 2.2362313270568848 },  
      { title: 'A Month in the Country', score: 2.2362313270568848 },  
      { title: 'A Quiet Place in the Country', score: 2.01576566696167 },  
      { title: 'A Sunday in the Country', score: 2.2362313270568848 }  
    ]  
  
#### Compound Search and Sort

The following query uses the `$search` stage to do the following:

  * Search for movies that have the term `dance` in the title, with a preference for movies that have won 2 or more awards and were released after 01 January, 1990.

  * Sort the results by the number of awards in descending order, then by the movie title in ascending order, and then by the release date in descending order.

The query uses the `$limit` stage to limit the output to `10` documents. It
also uses the `$project` stage to do the following:

  * Omit all fields except `title`, `released`, and `awards.wins` in the results.

  * Add a field named `score`.

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "compound": {  
            "must": [{  
              "text": {  
                "path": "title",  
                "query": "dance"  
              }  
            }],  
            "should": [{  
              "range": {  
                "path": "awards.wins",  
                "gte": 2  
              }  
            }, {  
              "range": {  
                "path": "released",  
                "gte": ISODate("1990-01-01T00:00:00.000Z")  
              }  
            }]  
          },  
          "sortBetaV1": {  
            "awards.wins": -1,  
            "title": 1,  
            "released": -1  
          }  
        }  
      },  
      {  
        "$limit": 10  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1,  
          "released": 1,  
          "awards.wins": 1,  
          "score": { "$meta": "searchScore" }  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        title: 'Shall We Dance?',  
        released: ISODate("1997-07-11T00:00:00.000Z"),  
        awards: { wins: 57 },  
        score: 3.9811458587646484  
      },  
      {  
        title: 'Shall We Dance?',  
        released: ISODate("1997-07-11T00:00:00.000Z"),  
        awards: { wins: 57 },  
        score: 3.9811458587646484  
      },  
      {  
        title: 'War Dance',  
        released: ISODate("2008-11-01T00:00:00.000Z"),  
        awards: { wins: 11 },  
        score: 4.466421127319336  
      },  
      {  
        title: 'Dance with the Devil',  
        released: ISODate("1997-10-31T00:00:00.000Z"),  
        awards: { wins: 6 },  
        score: 3.615056037902832  
      },  
      {  
        title: 'Save the Last Dance',  
        released: ISODate("2001-01-12T00:00:00.000Z"),  
        awards: { wins: 6 },  
        score: 3.615056037902832  
      },  
      {  
        title: 'Dance with a Stranger',  
        released: ISODate("1985-08-09T00:00:00.000Z"),  
        awards: { wins: 4 },  
        score: 3.615056037902832  
      },  
      {  
        title: 'The Baby Dance',  
        released: ISODate("1998-08-23T00:00:00.000Z"),  
        awards: { wins: 4 },  
        score: 3.9811458587646484  
      },  
      {  
        title: 'Three-Step Dance',  
        released: ISODate("2004-02-19T00:00:00.000Z"),  
        awards: { wins: 4 },  
        score: 3.9811458587646484  
      },  
      {  
        title: "Cats Don't Dance",  
        released: ISODate("1997-03-26T00:00:00.000Z"),  
        awards: { wins: 3 },  
        score: 3.9811458587646484  
      },  
      {  
        title: 'Dance Me Outside',  
        released: ISODate("1995-03-10T00:00:00.000Z"),  
        awards: { wins: 3 },  
        score: 3.9811458587646484  
      }  
    ]

