Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# facet

Share Feedback

On this page

  * Definition
  * Syntax
  * Fields
  * Facet Definition
  * String Facets
  * Numeric Facets
  * Date Facets
  * Facet Results
  * `SEARCH_META` Aggregation Variable
  * Limitations
  * Examples

`facet` is only available on Atlas clusters running one of the following
versions:

  * MongoDB 4.4.11 or later

  * MongoDB 5.0.4 or later

  * MongoDB 6.0 (including release candidates)

## Note

To run facet queries over sharded collections, your cluster must run MongoDB
v6.0 or higher.

You can't run `facet` queries with Retrieve Query Plan and Execution
Statistics.

## Definition

`facet`

    

The `facet` collector groups results by values or ranges in the specified
faceted fields and returns the count for each of those groups.

You can use `facet` with both the `$search` and `$searchMeta` stages. MongoDB
recommends using `facet` with the `$searchMeta` stage to retrieve metadata
results only for the query. To retrieve metadata results and query results
using the `$search` stage, you must use the `$$SEARCH_META` aggregation
variable. See `SEARCH_META` Aggregation Variable to learn more.

## Syntax

`facet` has the following syntax:

    
    
    {  
      
      "$searchMeta"|"$search": {  
        "index": <index name>, // optional, defaults to "default"  
        "facet": {  
          "operator": {  
            <operator-specifications>  
          },  
          "facets": {  
            <facet-definitions>  
          }  
        }  
      }  
    }  
  
## Fields

Field

|

Type

|

Required?

|

Description  
  
|||  
  
`facets`

|

document

|

yes

|

Information for bucketing the data for each facet. You must specify at least
one Facet Definition.  
  
`operator`

|

document

|

yes

|

Operator to use to perform the facet over.  
  
## Facet Definition

The facet definition document contains the facet name and options specific to
a type of facet. Atlas Search supports the following types of facets:

  * String Facets

  * Numeric Facets

  * Date Facets

### String Facets

String facets allow you to narrow down Atlas Search results based on the most
frequent string values in the specified string field. Note that the string
field must be indexed as How to Index String Fields For Faceted Search.

#### Syntax

String facets have the following syntax:

    
    
    {  
      
      "$searchMeta": {  
        "facet":{  
          "operator": {  
            <operator-specification>  
          },  
          "facets": {  
            "<facet-name>" : {  
              "type" : "string",  
              "path" : "<field-path>",  
              "numBuckets" : <number-of-categories>,  
            }  
          }  
        }  
      }  
    }  
  
#### Options

Option

|

Type

|

Description

|

Required?  
  
|||  
  
`numBuckets`

|

int

|

Maximum number of facet categories to return in the results. Value must be
less than or equal to `1000`. If specified, Atlas Search may return fewer
categories than requested if the data is grouped into fewer categories than
your requested number. If omitted, defaults to `10`, which means that Atlas
Search will return only the top `10` facet categories by count.

|

no  
  
`path`

|

string

|

Field path to facet on. You can specify a field that is indexed as a How to
Index String Fields For Faceted Search.

|

yes  
  
`type`

|

string

|

Type of facet. Value must be `string`.

|

yes  
  
#### Example

## Example

The following example uses an index named `default` on the
`sample_mflix.movies` collection. The `genres` field in the collection is
indexed as type How to Index String Fields For Faceted Search and the `year`
field is indexed as How to Index Numeric Values.

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "genres": {  
            "type": "stringFacet"  
          },  
          "year": {  
            "type": "number"  
          }  
        }  
      }  
    }  
  
The query uses the `$searchMeta` stage to search the `year` field in the
`movies` collection for movies from 2000 to 2015 and retrieve a count of the
number of movies in each genre.

    
    
    db.movies.aggregate([  
      
      {  
        "$searchMeta": {  
          "facet": {  
            "operator": {  
              "range": {  
                "path": "year",  
                "gte": 2000,  
                "lte": 2015  
              }  
            },  
            "facets": {  
              "genresFacet": {  
                "type": "string",  
                "path": "genres"  
              }  
            }  
          }  
        }  
      }  
    ])  
  
This query returns the following results:

    
    
    [  
      
      {  
        count: { lowerBound: Long("13718") },  
        facet: {  
          genresFacet: {  
            buckets: [  
              { _id: 'Drama', count: Long("7759") },  
              { _id: 'Comedy', count: Long("3937") },  
              { _id: 'Romance', count: Long("1916") },  
              { _id: 'Thriller', count: Long("1705") },  
              { _id: 'Documentary', count: Long("1703") },  
              { _id: 'Action', count: Long("1558") },  
              { _id: 'Crime', count: Long("1475") },  
              { _id: 'Adventure', count: Long("1111") },  
              { _id: 'Horror', count: Long("1008") },  
              { _id: 'Biography', count: Long("877") }  
            ]  
          }  
        }  
      }  
    ]  
  
To learn more about these results, see Facet Results.

### Numeric Facets

Numeric facets allow you to determine the frequency of numeric values in your
search results by breaking the results into separate ranges of numbers.

#### Syntax

Numeric facets have the following syntax:

    
    
    {  
      
      "$searchMeta": {  
        "facet":{  
          "operator": {  
            <operator-specification>  
          },  
          "facets": {  
            "<facet-name>" : {  
              "type" : "number",  
              "path" : "<field-path>",  
              "boundaries" : <array-of-numbers>,  
              "default": "<bucket-name>"  
            }  
          }  
        }  
      }  
    }  
  
#### Options

Option

|

Type

|

Description

|

Required?  
  
|||  
  
`boundaries`

|

array of numbers

|

List of numeric values, in ascending order, that specify the boundaries for
each bucket. You must specify at least two boundaries. Each adjacent pair of
values acts as the inclusive lower bound and the exclusive upper bound for the
bucket. You can specify any combination of values of the following BSON types:

  * 32-bit integer (`int32`)

  * 64-bit integer (`int64`)

  * 64-bit binary floating point (`double`)

|

yes  
  
`default`

|

string

|

Name of an additional bucket that counts documents returned from the operator
that do not fall within the specified boundaries. If omitted, Atlas Search
includes the results of the facet operator that do not fall under a specified
bucket also, but doesn't include it in any bucket counts.

|

no  
  
`path`

|

string

|

Field path to facet on. You can specify a field that is indexed as a How to
Index Numeric Values.

|

yes  
  
`type`

|

string

|

Type of facet. Value must be `number`.

|

yes  
  
#### Example

## Example

The following example uses an index named `default` on the
`sample_mflix.movies` collection. The `year` field in the collection is
indexed as type How to Index Numeric Values.

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "year": [  
            {  
              "type": "numberFacet"  
            }  
          ]  
        }  
      }  
    }  
  
The query uses the `$searchMeta` stage to search the `year` field in the
`movies` collection for movies between the years `1980` to `2000` and retrieve
metadata results for the query. The query specifies three buckets:

  * `1980`, inclusive lower bound for this bucket

  * `1990`, exclusive upper bound for the `1980` bucket and inclusive lower bound for this bucket

  * `2000`, exclusive upper bound for the `1990` bucket

The query also specifies a `default` bucket named `other` to retrieve results
of the query that don't fall under any of the specified boundaries.

    
    
    db.movies.aggregate([  
      
      {  
        "$searchMeta": {  
          "facet": {  
            "operator": {  
              "range": {  
                "path": "year",  
                "gte": 1980,  
                "lte": 2000  
              }  
            },  
            "facets": {  
              "yearFacet": {  
                "type": "number",  
                "path": "year",  
                "boundaries": [1980,1990,2000],  
                "default": "other"  
              }  
            }  
          }  
        }  
      }  
    ])  
  
This query returns the following results:

    
    
    [  
      
      {  
        "count" : {  
          "lowerBound" : NumberLong(6472)  
        },  
        "facet" : {  
          "yearFacet" : {  
            "buckets" : [  
              { "_id" : 1980, "count" : NumberLong(2081) },  
              { "_id" : 1990, "count" : NumberLong(3773) },  
              { "_id" : "other", "count" : NumberLong(618) }  
            ]  
          }  
        }  
      }  
    ]  
  
To learn more about these results, see Facet Results.

### Date Facets

Date facets allow you to narrow down search results based on a date.

#### Syntax

Date facets have the following syntax:

    
    
    {  
      
      "$searchMeta": {  
        "facet":{  
          "operator": {  
            <operator-specification>  
          },  
          "facets": {  
            "<facet-name>" : {  
              "type" : "date",  
              "path" : "<field-path>",  
              "boundaries" : <array-of-dates>,  
              "default": "<bucket-name>"  
            }  
          }  
        }  
      }  
    }  
  
#### Options

Option

|

Type

|

Description

|

Required?  
  
|||  
  
`boundaries`

|

array of numbers

|

List of date values that specify the boundaries for each bucket. You must
specify:

  * At least two boundaries

  * Values in ascending order, with the earliest date first

Each adjacent pair of values acts as the inclusive lower bound and the
exclusive upper bound for the bucket.

|

yes  
  
`default`

|

string

|

Name of an additional bucket that counts documents returned from the operator
that do not fall within the specified boundaries. If omitted, Atlas Search
includes the results of the facet operator that do not fall under a specified
bucket also, but Atlas Search doesn't include these results in any bucket
counts.

|

no  
  
`path`

|

string

|

Field path to facet on. You can specify a field that is indexed as a How to
Index Date Fields.

|

yes  
  
`type`

|

string

|

Type of facet. Value must be `date`.

|

yes  
  
#### Example

## Example

The following example uses an index named `default` on the
`sample_mflix.movies` collection. The `released` field in the collection is
indexed as type How to Index Date Fields.

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "released": [  
            {  
              "type": "dateFacet"  
            }  
          ]  
        }  
      }  
    }  
  
The query uses the `$searchMeta` stage to search the `released` field in the
`movies` collection for movies between the years `2000` to `2015` and retrieve
metadata results for the query string. The query specifies four buckets:

  * `2000-01-01`, inclusive lower bound for this bucket

  * `2005-01-01`, exclusive upper bound for the `2000-01-01` bucket and inclusive lower bound for this bucket

  * `2010-01-01`, exclusive upper bound for the `2005-01-01` bucket and inclusive lower bound for this bucket

  * `2015-01-01`, exclusive upper bound for the `2010-01-01` bucket

The query also specifies a `default` bucket named `other` to retrieve results
of the query that don't fall under any of the specified boundaries.

    
    
    db.movies.aggregate([  
      
      {  
        "$searchMeta": {  
          "facet": {  
            "operator": {  
              "range": {  
                "path": "released",  
                "gte": ISODate("2000-01-01T00:00:00.000Z"),  
                "lte": ISODate("2015-01-31T00:00:00.000Z")  
              }  
            },  
            "facets": {  
              "yearFacet": {  
                "type": "date",  
                "path": "released",  
                "boundaries": [ISODate("2000-01-01"), ISODate("2005-01-01"), ISODate("2010-01-01"), ISODate("2015-01-01")],  
                "default": "other"  
              }  
            }  
          }  
        }  
      }  
    ])  
  
This query returns the following results:

    
    
    [  
      
      {  
        "count" : {  
          "lowerBound" : NumberLong(13064)  
        },  
        "facet" : {  
          "releaseFacet" : {  
            "buckets" : [  
              {  
                "_id" : ISODate("2000-01-01T00:00:00Z"),  
                "count" : NumberLong(3242)  
              },  
              {  
                "_id" : ISODate("2005-01-01T00:00:00Z"),  
                "count" : NumberLong(4266)  
              },  
              {  
                "_id" : ISODate("2010-01-01T00:00:00Z"),  
                "count" : NumberLong(5445)  
              },  
              {  
                "_id" : "other",  
                "count" : NumberLong(111)  
              }  
            ]  
          }  
        }  
      }  
    ]  
  
To learn more about these results, see Facet Results.

## Facet Results

For a facet query, Atlas Search returns a mapping of the defined facet names
to an array of buckets for that facet in the results. The facet result
document contains the `buckets` option, which is an array of resulting buckets
for the facet. Each facet bucket document in the array has the following
fields:

Option

|

Type

|

Description  
  
||  
  
`_id`

|

object

|

Unique identifier that identifies this facet bucket. This value matches the
type of data that is being faceted on.  
  
`count`

|

int

|

Count of documents in this facet bucket. To learn more about the `count`
field, see Count Atlas Search Results.  
  
## `SEARCH_META` Aggregation Variable

When you run your query using the `$search` stage, Atlas Search stores the
metadata results in the `$$SEARCH_META` variable and returns only the search
results. You can use the `$$SEARCH_META` variable in all the supported
aggregation pipeline stages to view the metadata results for your `$search`
query.

MongoDB recommends using the `$$SEARCH_META` variable only if you need both
the search results and the metadata results. Otherwise, use the:

  * `$search` stage for just the search results.

  * `$searchMeta` stage for just the metadata results.

## Limitations

The following limitations apply:

  * You can run facet queries on a single field only. You can't run facet queries on groups of fields.

  * You can run facet queries over sharded collections on clusters running MongoDB v6.0 only.

## Examples

The following examples use the `sample_mflix.movies` collection. The metadata
results example demonstrates how to run a `$searchMeta` query with `facet` to
retrieve only the metadata in the results. The metadata and search results
example demonstrates how to run a `$search` query with `facet` and the
`$SEARCH_META` aggregation variable to retrieve both the search and metadata
results.

Metadata Results Example

Metadata and Search Results Example

The index definition specifies the following for the fields to index:

Field Name

|

Data Type  
  
|  
  
`directors`

|

How to Index String Fields For Faceted Search  
  
`year`

|

How to Index Numeric Values for Faceted Search  
  
`released`

|

How to Index Date Fields  
      
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "directors": {  
            "type": "stringFacet"  
          },  
          "year": {  
            "type": "numberFacet"  
          },  
          "released": {  
            "type": "date"  
          }  
        }  
      }  
    }  
  
The following query searches for movies released between January 01, 2000 and
January 31, 2015. It requests metadata on the `directors` and `year` field.

    
    
    db.movies.aggregate([  
      
      {  
        "$searchMeta": {  
          "facet": {  
            "operator": {  
              "range": {  
                "path": "released",  
                "gte": ISODate("2000-01-01T00:00:00.000Z"),  
                "lte": ISODate("2015-01-31T00:00:00.000Z")  
              }  
            },  
            "facets": {  
              "directorsFacet": {  
                "type": "string",  
                "path": "directors",  
                "numBuckets" : 7  
              },  
              "yearFacet" : {  
                "type" : "number",  
                "path" : "year",  
                "boundaries" : [2000,2005,2010, 2015]  
              }  
            }  
          }  
        }  
      }  
    ])  
  
Atlas Search returns the following results:

    
    
    [  
      
      {  
        "count" : { "lowerBound" : NumberLong(13064) },  
        "facet" : {  
          "yearFacet" : {  
            "buckets" : [  
              { "_id" : 2000, "count" : NumberLong(3283) },  
              { "_id" : 2005, "count" : NumberLong(4365) },  
              { "_id" : 2010, "count" : NumberLong(5123) }  
            ]  
          },  
          "directorsFacet" : {  
            "buckets" : [  
             { "_id" : "Takashi Miike", "count" : NumberLong(29) },  
              { "_id" : "Johnnie To", "count" : NumberLong(23) },  
              { "_id" : "Steven Soderbergh", "count" : NumberLong(21) },  
              { "_id" : "Michael Winterbottom", "count" : NumberLong(19) },  
              { "_id" : "Ken Loach", "count" : NumberLong(16) },  
              { "_id" : "Ki-duk Kim", "count" : NumberLong(16) },  
              { "_id" : "Ridley Scott", "count" : NumberLong(15) }  
            ]  
          }  
        }  
      }  
    ]  
  
The results show a count of the following in the `sample_mflix.movies`
collection:

  * Number of movies from the year 2000, inclusive lower bound, to 2015, exclusive upper bound, that Atlas Search returned for the query

  * Number of movies for each director that Atlas Search returned for the query

To learn more about these results, see Facet Results.

← existsgeoShape →

