Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# geoShape

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Examples

## Definition

`geoShape`

    

The `geoShape` operator supports querying shapes with a relation to a given
geometry if `indexShapes` is set to `true` in the index definition.

When specifying the coordinates to search, longitude must be specified first
and then the latitude. Longitude values can be between `-180` and `180`, both
inclusive. Latitude values can be between `-90` and `90`, both inclusive.
Coordinate values can be integers or doubles.

## Note

Atlas Search does not support the following:

  * Non-default coordinate reference system (CRS)

  * Planar XY coordinate system (2 dimensional)

  * Coordinate pairs Point notation (that is, `pointFieldName: [12, 34]`)

## Syntax

    
    
    1| {  
    |  
    2|     "$search": {  
    3|        "index": <index name>, // optional, defaults to "default"  
    4|        "geoShape": {  
    5|           "path": "<field-to-search>",  
    6|           "relation": "contains | disjoint | intersects | within",  
    7|           "geometry": <GeoJSON-object>,  
    8|           "score": <score-options>  
    9|        }  
    10|     }  
    11| }  
  
## Options

`geoShape` uses the following terms to construct a query:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`geometry`

|

GeoJSON object

|

GeoJSON object that specifies the Polygon, MultiPolygon, or LineString shape
or point to search. The polygon must be specified as a closed loop where the
last position is the same as the first position.

When calculating geospatial results, Atlas Search geoShape and geoWithin
operators and MongoDB $geoIntersects operator use different geometries. This
difference can be seen in how Atlas Search and MongoDB draw polygonal edges.

Atlas Search draws polygons based on Cartesian distance, which is the shortest
line between two points in the coordinate reference system.

MongoDB draws polygons using third-party library for geodesic types that use
geodesic lines. To learn more, see GeoJSON Objects.

Atlas Search and MongoDB could return different results for geospatial queries
involving polygons.

|

yes  
  
`path`

|

string or array of strings

|

Indexed geo type field or fields to search. See Path Construction for more
information.

|

yes  
  
`relation`

|

enum

|

Relation of the query shape geometry to the indexed field geometry. Value can
be one of the following:

  * `contains` \- Indicates that the indexed geometry contains the query geometry.

  * `disjoint` \- Indicates that both the query and indexed geometries have nothing in common.

  * `intersects` \- Indicates that both the query and indexed geometries intersect.

  * `within` \- Indicates that the indexed geometry is within the query geometry. You can't use `within` with `LineString` or `Point`.

|

yes  
  
`score`

|

object

|

Score assigned to matching search results. The score in the results is always
`1`. You can modify the score using the following options:

  * `boost`: multiply the result score by the given number.

  * `constant`: replace the result score with the given number.

For information on using `score` in your query, see Customize and Normalize
the Score in Results.

|

no  
  
## Examples

The following examples use the `listingsAndReviews` collection in the
`sample_airbnb` database. If you have the sample dataset on your cluster, you
can create a custom Atlas Search index for geo type and run the example
queries on your cluster.

## Tip

If you've already loaded the sample dataset, follow the Get Started with Atlas
Search tutorial to create an index definition and run Atlas Search queries.

The following is a sample index definition for indexing the `address.location`
field in the `listingsAndReviews` collection:

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "fields": {  
    4|       "address": {  
    5|         "fields": {  
    6|           "location": {  
    7|             "indexShapes": true,  
    8|             "type": "geo"  
    9|           }  
    10|         },  
    11|         "type": "document"  
    12|       }  
    13|     }  
    14|   }  
    15| }  
  
The Get Started with Atlas Search contains instructions for loading the sample
dataset, creating an index definition, and running Atlas Search queries.

## Note

For the following sample queries, make sure that `indexShapes` in the index
definition is set to `true`.

### Disjoint Example

The following example uses the `geoShape` operator to search for properties
that have nothing in common with the specified longitude and latitude
coordinates in Hawaii.

The query includes a:

  * `$limit` stage to limit the output to `3` results.

  * `$project` stage to exclude all fields except `name` and `address`.

    
    
    1| db.listingsAndReviews.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "geoShape": {  
    5|         "relation": "disjoint",  
    6|         "geometry": {  
    7|           "type": "Polygon",  
    8|           "coordinates": [[[-161.323242,22.512557],  
    9|                          [-152.446289,22.065278],  
    10|                          [-156.09375,17.811456],  
    11|                          [-161.323242,22.512557]]]  
    12|         },  
    13|         "path": "address.location"  
    14|       }  
    15|     }  
    16|   },  
    17|   {  
    18|     $limit: 3  
    19|   },  
    20|   {  
    21|     $project: {  
    22|       "_id": 0,  
    23|       "name": 1,  
    24|       "address": 1,  
    25|       score: { $meta: "searchScore" }  
    26|     }  
    27|   }  
    28| ])  
  
The query returns the following search results:

    
    
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
    15|   }  
    16| }  
    17| {  
    18|   "name" : "Horto flat with small garden",  
    19|   "address" : {  
    20|     "street" : "Rio de Janeiro, Rio de Janeiro, Brazil",  
    21|     "suburb" : "Jardim Botânico",  
    22|     "government_area" : "Jardim Botânico",  
    23|     "market" : "Rio De Janeiro",  
    24|     "country" : "Brazil",  
    25|     "country_code" : "BR",  
    26|     "location" : {  
    27|       "type" : "Point",  
    28|       "coordinates" : [ -43.23074991429229, -22.966253551739655 ],  
    29|       "is_location_exact" : true  
    30|     }  
    31|   }  
    32| }  
    33| {  
    34|   "name" : "Private Room in Bushwick",  
    35|   "address" : {  
    36|     "street" : "Brooklyn, NY, United States",  
    37|     "suburb" : "Brooklyn",  
    38|     "government_area" : "Bushwick",  
    39|     "market" : "New York",  
    40|     "country" : "United States",  
    41|     "country_code" : "US",  
    42|     "location" : {  
    43|       "type" : "Point",  
    44|       "coordinates" : [ -73.93615, 40.69791 ],  
    45|       "is_location_exact" : true  
    46|     }  
    47|   }  
    48| }  
  
### Intersects Example

The following example uses the `geoShape` operator to search for properties
that intersect with the specified longitude and latitude coordinates in Spain.

The query includes a:

  * `$limit` stage to limit the output to `3` results.

  * `$project` stage to exclude all fields except `name` and `address`.

    
    
    1| db.listingsAndReviews.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "geoShape": {  
    5|         "relation": "intersects",  
    6|         "geometry": {  
    7|           "type": "MultiPolygon",  
    8|           "coordinates": [  
    9|                        [[[2.16942,41.40082],  
    10|                        [2.17963,41.40087],  
    11|                        [2.18146,41.39716],  
    12|                        [2.15533,41.40686],  
    13|                        [2.14596,41.38475],  
    14|                        [2.17519,41.41035],  
    15|                        [2.16942,41.40082]]],  
    16|                        [[[2.16365,41.39416],  
    17|                        [2.16963,41.39726],  
    18|                        [2.15395,41.38005],  
    19|                        [2.17935,41.43038],  
    20|                        [2.16365,41.39416]]]  
    21|           ]  
    22|         },  
    23|         "path": "address.location"  
    24|       }  
    25|     }  
    26|   },  
    27|   {  
    28|     $limit: 3  
    29|   },  
    30|   {  
    31|     $project: {  
    32|       "_id": 0,  
    33|       "name": 1,  
    34|       "address": 1,  
    35|       score: { $meta: "searchScore" }  
    36|     }  
    37|   }  
    38| ])  
  
The query returns the following search results:

    
    
    1| {  
    |  
    2|   "name" : "Cozy bedroom Sagrada Familia",  
    3|   "address" : {  
    4|     "street" : "Barcelona, Catalunya, Spain",  
    5|     "suburb" : "Eixample",  
    6|     "government_area" : "el Fort Pienc",  
    7|     "market" : "Barcelona",  
    8|     "country" : "Spain",  
    9|     "country_code" : "ES",  
    10|     "location" : {  
    11|       "type" : "Point",  
    12|       "coordinates" : [ 2.17963, 41.40087 ],  
    13|       "is_location_exact" : true  
    14|     }  
    15|   }  
    16| }  
    17| {  
    18|   "name" : "",  
    19|   "address" : {  
    20|     "street" : "Barcelona, Catalunya, Spain",  
    21|     "suburb" : "Vila de Gràcia",  
    22|     "government_area" : "la Vila de Gràcia",  
    23|     "market" : "Barcelona",  
    24|     "country" : "Spain",  
    25|     "country_code" : "ES",  
    26|     "location" : {  
    27|       "type" : "Point",  
    28|       "coordinates" : [ 2.15759, 41.40349 ],  
    29|       "is_location_exact" : true  
    30|     }  
    31|   }  
    32| }  
    33| {  
    34|   "name" : "SPACIOUS RAMBLA CATALUÑA",  
    35|   "address" : {  
    36|     "street" : "Barcelona, Catalunya, Spain",  
    37|     "suburb" : "L'Antiga Esquerra de l'Eixample",  
    38|     "government_area" : "l'Antiga Esquerra de l'Eixample",  
    39|     "market" : "Barcelona",  
    40|     "country" : "Spain",  
    41|     "country_code" : "ES",  
    42|     "location" : {  
    43|       "type" : "Point",  
    44|       "coordinates" : [ 2.15255, 41.39193 ],  
    45|       "is_location_exact" : true  
    46|     }  
    47|   }  
    48| }  
  
### Within Example

The following example uses the `geoShape` operator to search for properties in
New York that are within the specified longitude and latitude coordinates. The
queries searches the `address.location` field in the `listingsAndReviews`
collection in the `sample_airbnb` database.

The query includes a:

  * `$limit` stage to limit the output to `3` results.

  * `$project` stage to exclude all fields except `name` and `address`.

    
    
    1| db.listingsAndReviews.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "geoShape": {  
    5|         "relation": "within",  
    6|         "geometry": {  
    7|           "type": "Polygon",  
    8|           "coordinates": [[[-74.3994140625,40.5305017757],  
    9|                          [-74.7290039063,40.5805846641],  
    10|                          [-74.7729492188,40.9467136651],  
    11|                          [-74.0698242188,41.1290213475],  
    12|                          [-73.65234375,40.9964840144],  
    13|                          [-72.6416015625,40.9467136651],  
    14|                          [-72.3559570313,40.7971774152],  
    15|                          [-74.3994140625,40.5305017757]]]  
    16|         },  
    17|         "path": "address.location"  
    18|       }  
    19|     }  
    20|   },  
    21|   {  
    22|     $limit: 3  
    23|   },  
    24|   {  
    25|     $project: {  
    26|       "_id": 0,  
    27|       "name": 1,  
    28|       "address": 1,  
    29|       score: { $meta: "searchScore" }  
    30|     }  
    31|   }  
    32| ])  
  
The query returns the following search results:

    
    
    1| {  
    |  
    2|   "name" : "Private Room in Bushwick",  
    3|   "address" : {  
    4|     "street" : "Brooklyn, NY, United States",  
    5|     "suburb" : "Brooklyn",  
    6|     "government_area" : "Bushwick",  
    7|     "market" : "New York",  
    8|     "country" : "United States",  
    9|     "country_code" : "US",  
    10|     "location" : {  
    11|       "type" : "Point",  
    12|       "coordinates" : [ -73.93615, 40.69791 ],  
    13|       "is_location_exact" : true  
    14|     }  
    15|   },  
    16|   {  
    17|     "name" : "New York City - Upper West Side Apt",  
    18|     "address" : {  
    19|       "street" : "New York, NY, United States",  
    20|       "suburb" : "Manhattan",  
    21|       "government_area" : "Upper West Side",  
    22|       "market" : "New York",  
    23|       "country" : "United States",  
    24|       "country_code" : "US",  
    25|       "location" : {  
    26|         "type" : "Point",  
    27|         "coordinates" : [ -73.96523, 40.79962 ],  
    28|         "is_location_exact" : false  
    29|       }  
    30|     },  
    31|     "score" : 1  
    32|   }  
    33|   {  
    34|     "name" : "Deluxe Loft Suite",  
    35|     "address" : {  
    36|       "street" : "Brooklyn, NY, United States",  
    37|       "suburb" : "Greenpoint",  
    38|       "government_area" : "Greenpoint",  
    39|       "market" : "New York",  
    40|       "country" : "United States",  
    41|       "country_code" : "US",  
    42|       "location" : {  
    43|         "type" : "Point",  
    44|         "coordinates" : [ -73.94472, 40.72778 ],  
    45|         "is_location_exact" : true  
    46|       }  
    47|     },  
    48|     "score" : 1  
    49|   }  
  
← facetgeoWithin →

