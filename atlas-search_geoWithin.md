Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# geoWithin

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Examples
  * `box` Example
  * `circle` Example
  * `geometry` Examples

## Definition

`geoWithin`

    

The `geoWithin` operator supports querying geographic points within a given
geometry. Only points are returned, even if `indexShapes` value is `true` in
the index definition.

You can query points within a:

  * Circle

  * Bounding box

  * Polygon

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

`geoWithin` has the following syntax:

    
    
    {  
      
      "$search": {  
         "index": <index name>, // optional, defaults to "default"  
         "geoWithin": {  
            "path": "<field-to-search>",  
            "box | circle | geometry": <object>,  
            "score": <score-options>  
         }  
      }  
    }  
  
## Options

`geoWithin` uses the following terms to construct a query:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`box`

|

object

|

Object that specifies the bottom left and top right GeoJSON points of a box to
search within. The object takes the following fields:

  * `bottomLeft` \- Bottom left GeoJSON point.

  * `topRight` \- Top right GeoJSON point.

To learn how to specify GeoJSON data inside a GeoJSON object, see GeoJSON
Objects.

Either `box`, `circle`, or `geometry` is required.

|

conditional  
  
`circle`

|

object

|

Object that specifies the center point and the radius in meters to search
within. The object contains the following GeoJSON fields:

  * `center` \- Center of the circle specified as a GeoJSON point.

  * `radius` \- Radius, which is a number, specified in meters. Value must be greater than or equal to `0`.

To learn how to specify GeoJSON data inside a GeoJSON object, see GeoJSON
Objects.

Either `circle`, `box`, or `geometry` is required.

|

conditional  
  
`geometry`

|

GeoJSON object

|

GeoJSON object that specifies the MultiPolygon or Polygon to search within.
The polygon must be specified as a closed loop where the last position is the
same as the first position.

When calculating geospatial results, Atlas Search geoShape and geoWithin
operators and MongoDB $geoIntersects operator use different geometries. This
difference can be seen in how Atlas Search and MongoDB draw polygonal edges.

Atlas Search draws polygons based on Cartesian distance, which is the shortest
line between two points in the coordinate reference system.

MongoDB draws polygons using third-party library for geodesic types that use
geodesic lines. To learn more, see GeoJSON Objects.

Atlas Search and MongoDB could return different results for geospatial queries
involving polygons.

To learn how to specify GeoJSON data inside a GeoJSON object, see GeoJSON
Objects.

Either `geometry`, `box`, or `circle` is required.

|

conditional  
  
`path`

|

string or array of strings

|

Indexed geo type field or fields to search. See Path Construction.

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

You can use any of the following sample datasets for running Atlas Search
queries with the `geoWithin` operator:

  * Sample AirBnB Listings Dataset

  * Sample Geospatial Dataset

  * Sample Restaurants Dataset

  * Sample Training Dataset Trips Collection

Use the following sample index definition for indexing the `address.location`
field in the `listingsAndReviews` collection:

    
    
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
    11|       }  
    12|     }  
    13|   }  
    14| }  
  
### `box` Example

The following query uses the `geoWithin` operator with the `box` field to
search for properties within a bounding box in Australia.

The query includes a:

  * `$limit` stage to limit the output to `3` results.

  * `$project` stage to exclude all fields except `name` and `address`.

## Note

You don't need to specify indexes named `default` in your Atlas Search query.
If your index has any other name, you must specify the `index` field.

    
    
    1| db.listingsAndReviews.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "geoWithin": {  
    5|         "path": "address.location",  
    6|         "box": {  
    7|           "bottomLeft": {  
    8|             "type": "Point",  
    9|             "coordinates": [112.467, -55.050]  
    10|           },  
    11|           "topRight": {  
    12|             "type": "Point",  
    13|             "coordinates": [168.000, -9.133]  
    14|           }  
    15|         }  
    16|       }  
    17|     }  
    18|   },  
    19|   {  
    20|     $limit: 3  
    21|   },  
    22|   {  
    23|     $project: {  
    24|       "_id": 0,  
    25|       "name": 1,  
    26|       "address": 1  
    27|     }  
    28|   }  
    29| ])  
  
The query returns the following results:

    
    
    1| {  
    |  
    2|   "name" : "Surry Hills Studio - Your Perfect Base in Sydney",  
    3|   "address" : {  
    4|     "street" : "Surry Hills, NSW, Australia",  
    5|     "suburb" : "Darlinghurst",  
    6|     "government_area" : "Sydney",  
    7|     "market" : "Sydney",  
    8|     "country" : "Australia",  
    9|     "country_code" : "AU",  
    10|     "location" : {  
    11|       "type" : "Point",  
    12|       "coordinates" : [ 151.21554, -33.88029 ],  
    13|       "is_location_exact" : true  
    14|     }  
    15|   }  
    16| }  
    17| {  
    18|   "name" : "Sydney Hyde Park City Apartment (checkin from 6am)",  
    19|   "address" : {  
    20|     "street" : "Darlinghurst, NSW, Australia",  
    21|     "suburb" : "Darlinghurst",  
    22|     "government_area" : "Sydney",  
    23|     "market" : "Sydney",  
    24|     "country" : "Australia",  
    25|     "country_code" : "AU",  
    26|     "location" : {  
    27|       "type" : "Point",  
    28|       "coordinates" : [ 151.21346, -33.87603 ],  
    29|       "is_location_exact" : false  
    30|     }  
    31|   }  
    32| }  
    33| {  
    34|   "name" : "THE Place to See Sydney's FIREWORKS",  
    35|   "address" : {  
    36|     "street" : "Rozelle, NSW, Australia",  
    37|     "suburb" : "Lilyfield/Rozelle",  
    38|     "government_area" : "Leichhardt",  
    39|     "market" : "Sydney",  
    40|     "country" : "Australia",  
    41|     "country_code" : "AU",  
    42|     "location" : {  
    43|       "type" : "Point",  
    44|       "coordinates" : [ 151.17956, -33.86296 ],  
    45|       "is_location_exact" : true  
    46|     }  
    47|   }  
    48| }  
  
### `circle` Example

The following query uses the `geoWithin` operator with the `circle` field to
search for properties within one mile radius of specified coordinates in
Canada.

The query includes a:

  * `$limit` stage to limit the output to `3` results

  * `$project` stage to exclude all fields except `name` and `address`.

## Note

You don't need to specify indexes named `default` in your Atlas Search query.
If your index has any other name, you must specify the `index` field.

    
    
    1| db.listingsAndReviews.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "geoWithin": {  
    5|         "circle": {  
    6|           "center": {  
    7|             "type": "Point",  
    8|             "coordinates": [-73.54, 45.54]  
    9|           },  
    10|           "radius": 1600  
    11|         },  
    12|         "path": "address.location"  
    13|       }  
    14|     }  
    15|   },  
    16|   {  
    17|     $limit: 3  
    18|   },  
    19|   {  
    20|     $project: {  
    21|       "_id": 0,  
    22|       "name": 1,  
    23|       "address": 1  
    24|     }  
    25|   }  
    26| ])  
  
The query returns the following results:

    
    
    1| {  
    |  
    2|   "name" : "Ligne verte - à 15 min de métro du centre ville.",  
    3|   "address" : {  
    4|     "street" : "Montréal, Québec, Canada",  
    5|     "suburb" : "Hochelaga-Maisonneuve",  
    6|     "government_area" : "Mercier-Hochelaga-Maisonneuve",  
    7|     "market" : "Montreal",  
    8|     "country" : "Canada",  
    9|     "country_code" : "CA",  
    10|     "location" : {  
    11|       "type" : "Point",  
    12|       "coordinates" : [ -73.54949, 45.54548 ],  
    13|       "is_location_exact" : false  
    14|     }  
    15|   }  
    16| }  
    17| {  
    18|   "name" : "Belle chambre à côté Metro Papineau",  
    19|   "address" : {  
    20|     "street" : "Montréal, QC, Canada",  
    21|     "suburb" : "Gay Village",  
    22|     "government_area" : "Ville-Marie",  
    23|     "market" : "Montreal",  
    24|     "country" : "Canada",  
    25|     "country_code" : "CA",  
    26|     "location" : {  
    27|       "type" : "Point",  
    28|       "coordinates" : [ -73.54985, 45.52797 ],  
    29|       "is_location_exact" : false  
    30|     }  
    31|   }  
    32| }  
    33| {  
    34|   "name" : "L'IDÉAL, ( à 2 min du métro Pie-IX ).",  
    35|   "address" : {  
    36|     "street" : "Montréal, Québec, Canada",  
    37|     "suburb" : "Mercier-Hochelaga-Maisonneuve",  
    38|     "government_area" : "Mercier-Hochelaga-Maisonneuve",  
    39|     "market" : "Montreal",  
    40|     "country" : "Canada",  
    41|     "country_code" : "CA",  
    42|     "location" : {  
    43|       "type" : "Point",  
    44|       "coordinates" : [ -73.55208, 45.55157 ],  
    45|       "is_location_exact" : true  
    46|     }  
    47|   }  
    48| }  
  
### `geometry` Examples

The following examples use the `geoWithin` operator with the `geometry` field
to search for properties in Hawaii. The `type` field specifies whether the
area is a GeoJSON Polygon or MultiPolygon.

The queries include a:

  * `$limit` stage to limit the output to `3` results.

  * `$project` stage to exclude all fields except `name` and `address`.

## Note

You don't need to specify indexes named `default` in your Atlas Search query.
If your index has any other name, you must specify the `index` field.

Polygon Example

MultiPolygon Example

    
    
    1|  db.listingsAndReviews.aggregate([  
    |  
    2|    {  
    3|      "$search": {  
    4|        "geoWithin": {  
    5|          "geometry": {  
    6|            "type": "Polygon",  
    7|            "coordinates": [[[ -161.323242, 22.512557 ],  
    8|                           [ -152.446289, 22.065278 ],  
    9|                           [ -156.09375, 17.811456 ],  
    10|                           [ -161.323242, 22.512557 ]]]  
    11|          },  
    12|          "path": "address.location"  
    13|        }  
    14|      }  
    15|    },  
    16|    {  
    17|      $limit: 3  
    18|    },  
    19|    {  
    20|      $project: {  
    21|        "_id": 0,  
    22|        "name": 1,  
    23|        "address": 1  
    24|      }  
    25|    }  
    26|  ])  
  
The query returns the following results:

    
    
    1| {  
    |  
    2|   "name" : "Ocean View Waikiki Marina w/prkg",  
    3|   "address" : {  
    4|     "street" : "Honolulu, HI, United States",  
    5|     "suburb" : "Oʻahu",  
    6|     "government_area" : "Primary Urban Center",  
    7|     "market" : "Oahu",  
    8|     "country" : "United States",  
    9|     "country_code" : "US",  
    10|     "location" : {  
    11|       "type" : "Point",  
    12|       "coordinates" : [ -157.83919, 21.28634 ],  
    13|       "is_location_exact" : true  
    14|     }  
    15|   }  
    16| }  
    17| {  
    18|   "name" : "Kailua-Kona, Kona Coast II 2b condo",  
    19|   "address" : {  
    20|     "street" : "Kailua-Kona, HI, United States",  
    21|     "suburb" : "Kailua/Kona",  
    22|     "government_area" : "North Kona",  
    23|     "market" : "The Big Island",  
    24|     "country" : "United States",  
    25|     "country_code" : "US",  
    26|     "location" : {  
    27|       "type" : "Point",  
    28|       "coordinates" : [ -155.96445, 19.5702 ],  
    29|       "is_location_exact" : true  
    30|     }  
    31|   }  
    32| }  
    33| {  
    34|   "name" : "LAHAINA, MAUI! RESORT/CONDO BEACHFRONT!! SLEEPS 4!",  
    35|   "address" : {  
    36|     "street" : "Lahaina, HI, United States",  
    37|     "suburb" : "Maui",  
    38|     "government_area" : "Lahaina",  
    39|     "market" : "Maui",  
    40|     "country" : "United States",  
    41|     "country_code" : "US",  
    42|     "location" : {  
    43|       "type" : "Point",  
    44|       "coordinates" : [ -156.68012, 20.96996 ],  
    45|       "is_location_exact" : true  
    46|     }  
    47|   }  
    48| }  
  
← geoShapemoreLikeThis →

