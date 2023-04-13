Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# near

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Limitation
  * Examples

## Definition

`near`

    

The `near` operator supports querying and scoring numeric, date, and GeoJSON
point values. This operator can be used to perform a search over:

  * Number fields of BSON `int32`, `int64`, and `double` data types.

  * Date fields of BSON `date` type in ISODate format.

  * Geographic location fields defined using latitude and longitude coordinates.

You can use the `near` operator to find results that are near a number or a
date. The `near` operator scores the Atlas Search results by proximity to the
number or date.

## Syntax

`near` has the following syntax:

    
    
    {  
      
       $search: {  
          "index": <index name>, // optional, defaults to "default"  
          "near": {  
             "path": "<field-to-search>",  
             "origin": <date-or-number>,  
             "pivot": <pivot-distance>,  
             "score": <score-options>  
          }  
       }  
    }  
  
## Options

`near` uses the following terms to construct a query:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`origin`

|

date, number, or geo

|

Number, date, or geographic point to search near. This is the origin from
which the proximity of the results is measured.

  * For number fields, the value must be of BSON `int32`, `int64`, or `double` data types.

  * For date fields, the value must be an ISODate formatted date.

  * For geo fields. the value must be a GeoJSON point.

|

yes  
  
`path`

|

string or array of strings

|

Indexed field or fields to search. See Path Construction.

|

yes  
  
`pivot`

|

number

|

Value to use to calculate scores of Atlas Search result documents. Score is
calculated using the following formula:

    
    
    |               pivot  
      
    score =   
             pivot + distance  
  
where `distance` is the difference between `origin` and the indexed field
value.

Results have a score equal to `1/2` (or `0.5`) when their indexed field value
is `pivot` units away from `origin`. The value of `pivot` must be greater than
(i.e. `>`) `0`.

If `origin` is a:

  * Number, `pivot` can be specified as an integer or floating point number.

  * Date, `pivot` must be specified in milliseconds and can be specified as a 32 or 64 bit integer.

## Example

    * 1 minute is equal to `60,000 ms`

    * 1 hour is equal to `3,600,000 ms`

    * 1 day is equal to `86,400,000 ms`

    * 1 month (or 30 days) is equal to `2,592,000,000 ms`

  * GeoJSON point, `pivot` is measured in meters and must be specified as an integer or floating point number.

yes  
  
`score`

|

object

|

A measure of the proximity of the Atlas Search results to `origin`. The
`score` is scaled between `0` and `1` with `1` being an exact match and `0`
being a distant match. Score is equal to `0.5` when the distance of the Atlas
Search result from `origin` is equal to the distance away from origin as
calculated using `pivot`.

Score is calculated using the following formula:

    
    
    |               pivot  
      
    score =   
             pivot + distance  
  
where `distance` is the difference between `origin` and the indexed field
value.

You can modify the score of the matching search results using the following
options:

  * `boost`: multiply the result score by the given number.

  * `constant`: replace the result score with the given number.

For more information on using `score` in your query, see Customize and
Normalize the Score in Results.

no  
  
## Limitation

You can't use the `near` operator to query numeric or date values stored in an
array, even if you have an Atlas Search index. You can use the range operator
only to query indexed numeric or date values inside arrays.

## Examples

The number and date examples use the `movies` collection in the `sample_mflix`
database. The GeoJSON point example uses the `listingsAndReviews` collection
in the `sample_airbnb` database.

If you load the sample data on your Atlas cluster, you can create the static
indexes using the index definitions in the examples below or the dynamic index
and run the example queries on your cluster.

## Tip

If you've already loaded the sample dataset, follow the Get Started with Atlas
Search tutorial to create an index definition and run Atlas Search queries.

### Number Example

The following example uses the `near` operator to query a number field.

## Example

The following index definition named `runtimes` indexes the `runtime` field
values in the `movies` collection:

    
    
    1| {  
    |  
    2|    "mappings": {  
    3|       "dynamic": false,  
    4|       "fields": {  
    5|          "runtime": {  
    6|             "type": "number"  
    7|          }  
    8|       }  
    9|    }  
    10| }  
  
The following query searches for documents in the `movies` collection with a
`runtime` field value that is near 279. It includes a `$limit` stage to limit
the output to 7 results and a `$project` stage to:

  * Exclude all fields except `title` and `runtime`

  * Add a field named `score`

The `score` is calculated using `pivot`.

    
    
    1| db.movies.aggregate([  
    |  
    2|    {  
    3|       $search: {  
    4|          "index": "runtimes",  
    5|          "near": {  
    6|             "path": "runtime",  
    7|             "origin": 279,  
    8|             "pivot": 2  
    9|          }  
    10|       }  
    11|    },  
    12|    {  
    13|       $limit: 7  
    14|    },  
    15|    {  
    16|       $project: {  
    17|          "_id": 0,  
    18|          "title": 1,  
    19|          "runtime": 1,  
    20|          score: { $meta: "searchScore" }  
    21|       }  
    22|    }  
    23| ])  
  
The above query returns the following results:

    
    
    1| { "runtime" : 279, "title" : "The Kingdom", "score" : 1 }  
    |  
    2| { "runtime" : 279, "title" : "The Jinx: The Life and Deaths of Robert Durst", "score" : 1 }  
    3| { "runtime" : 280, "title" : "Shoah", "score" : 0.6666666865348816 }  
    4| { "runtime" : 281, "title" : "Les Misèrables", "score" : 0.5 }  
    5| { "runtime" : 277, "title" : "Tokyo Trial", "score" : 0.5 }  
    6| { "runtime" : 276, "title" : "Warriors of the Rainbow: Seediq Bale", "score" : 0.4000000059604645 }  
    7| { "runtime" : 283, "title" : "Scenes from a Marriage", "score" : 0.3333333432674408 }  
  
In the above Atlas Search results, the movies `The Kingdom` and `The Jinx: The
Life and Deaths of Robert Durst` receive a score of `1.0` because their
`runtime` field value of `279` is an exact match. The movies `Les Misèrables`
and `Tokyo Trial` receive a score of `0.5` because their `runtime` field value
is `2` units away from `279`.

### Date Example

The following example uses the `near` operator to query a date field.

## Example

The following index definition named `releaseddate` indexes the `released`
field values in the `movies` collection:

    
    
    1| {  
    |  
    2|    "mappings": {  
    3|       "dynamic": false,  
    4|       "fields": {  
    5|          "released": {  
    6|             "type": "date"  
    7|          }  
    8|       }  
    9|    }  
    10| }  
  
The following query searches for movies released near September 13, 1\. It
includes a `$limit` stage to limit the output to `3` results and a `$project`
stage to:

  * Exclude all fields except `title` and `released`

  * Add a field named `score`

The `score` of results is calculated using `pivot`.

## Note

`pivot` is measured here in milliseconds, and `7,776,000,000 ms` is equal to
approximately three months.

    
    
    1| db.movies.aggregate([  
    |  
    2|    {  
    3|       $search: {  
    4|          "index": "releaseddate",  
    5|          "near": {  
    6|             "path": "released",  
    7|             "origin": ISODate("1915-09-13T00:00:00.000+00:00"),  
    8|             "pivot": 7776000000  
    9|          }  
    10|       }  
    11|    },  
    12|    {  
    13|       $limit: 3  
    14|    },  
    15|    {  
    16|       $project: {  
    17|          "_id": 0,  
    18|          "title": 1,  
    19|          "released": 1,  
    20|          score: { $meta: "searchScore" }  
    21|       }  
    22|    }  
    23| ])  
  
The above query returns the following search results:

    
    
    { "title" : "Regeneration", "released" : ISODate("1915-09-13T00:00:00Z"), "score" : 1 }  
      
    { "title" : "The Cheat", "released" : ISODate("1915-12-13T00:00:00Z"), "score" : 0.49723756313323975 }  
    { "title" : "Hell's Hinges", "released" : ISODate("1916-03-05T00:00:00Z"), "score" : 0.34090909361839294 }  
  
In the above Atlas Search results, the movie `Regeneration` receives a score
of `1` because the `released` field value of `1915-09-13` is an exact match.
The movie `The Cheat`, which was released on `1915-12-13`, receives a score of
approximately `0.5` because the `released` field value distance from `origin`
is approximately `7,776,000,000` milliseconds from `1915-09-13`.

### GeoJSON Point Examples

The following examples use the `near` operator to query a GeoJSON point object
in the `sample_airbnb.listingsAndReviews` collection. The following index
definition indexes the `address.location` and `property_type` fields in the
`listingsAndReviews` collection.

## Example

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "fields": {  
    4|       "address": {  
    5|         "fields": {  
    6|           "location": {  
    7|             "type": "geo"  
    8|           }  
    9|         },  
    10|         "type": "document"  
    11|       },  
    12|       "property_type": {  
    13|         "type": "string"  
    14|       }  
    15|     }  
    16|   }  
    17| }  
  
#### Basic Example

The following examples use the `near` operator to query the `address.location`
field in the `sample_airbnb.listingsAndReviews` collection.

## Example

The following query searches for properties in Portugal. It includes a
`$limit` stage to limit the output to `3` results and a $project stage to:

  * Exclude all fields except `name` and `address`

  * Add a field named `score`

The `score` of results is calculated using `pivot`. Note that `pivot` is
measured here in meters and 1000 meters is equal to 1 kilometer.

    
    
    1| db.listingsAndReviews.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "near": {  
    5|         "origin": {  
    6|           "type": "Point",  
    7|           "coordinates": [-8.61308, 41.1413]  
    8|         },  
    9|         "pivot": 1000,  
    10|         "path": "address.location"  
    11|       }  
    12|     }  
    13|   },  
    14|   {  
    15|     $limit: 3  
    16|   },  
    17|   {  
    18|     $project: {  
    19|       "_id": 0,  
    20|       "name": 1,  
    21|       "address": 1,  
    22|       score: { $meta: "searchScore" }  
    23|     }  
    24|   }  
    25| ])  
  
The above query returns the following search results:

    
    
    1| {  
    |  
    2|   "name" : "Ribeira Charming Duplex",  
    3|   "address" : {  
    4|     "street" : "Porto, Porto, Portugal",  
    5|     "suburb" : "",  
    6|     "government_area" : "Cedofeita, Ildefonso, Sé, Miragaia, Nicolau, Vitória",  
    7|     "market" : "Porto",  
    8|     "country" : "Portugal",  
    9|     "country_code" : "PT",  
    10|     "location" : {  
    11|       "type" : "Point",  
    12|       "coordinates" : [ -8.61308, 41.1413 ],  
    13|       "is_location_exact" : false  
    14|     }  
    15|   },  
    16|   "score" : 1  
    17| }  
    18| {  
    19|   "name" : "DB RIBEIRA - Grey Apartment",  
    20|   "address" : {  
    21|     "street" : "Porto, Porto, Portugal",  
    22|     "suburb" : "",  
    23|     "government_area" : "Cedofeita, Ildefonso, Sé, Miragaia, Nicolau, Vitória",  
    24|     "market" : "Porto",  
    25|     "country" : "Portugal",  
    26|     "country_code" : "PT",  
    27|     "location" : {  
    28|       "type" : "Point",  
    29|       "coordinates" : [ -8.61294, 41.14126 ],  
    30|       "is_location_exact" : true  
    31|     }  
    32|   },  
    33|   "score" : 0.9876177310943604  
    34| }  
    35| {  
    36|   "name" : "Ribeira 24 (4)",  
    37|   "address" : {  
    38|     "street" : "Porto, Porto, Portugal",  
    39|     "suburb" : "",  
    40|     "government_area" : "Cedofeita, Ildefonso, Sé, Miragaia, Nicolau, Vitória",  
    41|     "market" : "Porto",  
    42|     "country" : "Portugal",  
    43|     "country_code" : "PT",  
    44|     "location" : {  
    45|       "type" : "Point",  
    46|       "coordinates" : [ -8.61318, 41.14107 ],  
    47|       "is_location_exact" : false  
    48|     }  
    49|   },  
    50|   "score" : 0.973789632320404  
    51| }  
  
The results show that properties that are farther away from the specified
coordinates have a lower score.

#### Compound Example

The following example uses the `compound` operator to query the
`property_type` and `address.location` fields in the
`sample_airbnb.listingsAndReviews` collection.

## Example

The following query searches for apartments in Hong Kong near a specified
GeoJSON point. The query uses **must** to specify the search condition, which
must be met, and **should** to specify preference for location. It includes a
`$limit` stage to limit the output to 3 results and a $project stage to:

  * Exclude all fields except `property_type` and `address`

  * Add a field named `score`

The `score` is calculated using the `pivot` field. Note that `pivot` is
measured here in meters and 1000 meters is equal to 1 kilometer.

    
    
    1| db.listingsAndReviews.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "compound": {  
    5|         "must": {  
    6|           "text": {  
    7|             "query": "Apartment",  
    8|             "path": "property_type"  
    9|           }  
    10|         },  
    11|         "should": {  
    12|           "near": {  
    13|             "origin": {  
    14|               "type": "Point",  
    15|               "coordinates": [114.15027, 22.28158]  
    16|             },  
    17|             "pivot": 1000,  
    18|             "path": "address.location"  
    19|           }  
    20|         }  
    21|       }  
    22|     }  
    23|   },  
    24|   {  
    25|     $limit: 3  
    26|   },  
    27|   {  
    28|     $project: {  
    29|       "_id": 0,  
    30|       "property_type": 1,  
    31|       "address": 1,  
    32|       score: { $meta: "searchScore" }  
    33|     }  
    34|   }  
    35| ])  
  
The above query returns the following search results:

    
    
    1| {  
    |  
    2|   "property_type" : "Apartment",  
    3|   "address" : {  
    4|     "street" : "Hong Kong, Hong Kong Island, Hong Kong",  
    5|     "suburb" : "Central & Western District",  
    6|     "government_area" : "Central & Western",  
    7|     "market" : "Hong Kong",  
    8|     "country" : "Hong Kong",  
    9|     "country_code" : "HK",  
    10|     "location" : {  
    11|       "type" : "Point",  
    12|       "coordinates" : [ 114.15027, 22.28158 ],  
    13|       "is_location_exact" : true  
    14|     }  
    15|   },  
    16|   "score" : 1.177286982536316  
    17| }  
    18| {  
    19|   "property_type" : "Apartment",  
    20|   "address" : {  
    21|     "street" : "Hong Kong, Hong Kong Island, Hong Kong",  
    22|     "suburb" : "Central & Western District",  
    23|     "government_area" : "Central & Western",  
    24|     "market" : "Hong Kong",  
    25|     "country" : "Hong Kong",  
    26|     "country_code" : "HK",  
    27|     "location" : {  
    28|       "type" : "Point",  
    29|       "coordinates" : [ 114.15082, 22.28161 ],  
    30|       "is_location_exact" : true  
    31|     }  
    32|   },  
    33|   "score" : 1.1236450672149658  
    34| }  
    35| {  
    36|   "property_type" : "Apartment",  
    37|   "address" : {  
    38|     "street" : "Hong Kong,  
    39|     Hong Kong Island, Hong Kong",  
    40|     "suburb" : "Mid-Levels",  
    41|     "government_area" : "Central & Western",  
    42|     "market" : "Hong Kong",  
    43|     "country" : "Hong Kong",  
    44|     "country_code" : "HK",  
    45|     "location" : {  
    46|       "type" : "Point",  
    47|       "coordinates" : [ 114.15007, 22.28215 ],  
    48|       "is_location_exact" : true  
    49|     }  
    50|   },  
    51|   "score" : 1.114811897277832  
    52| }  
  
← moreLikeThisphrase →

