Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Use Facets with Atlas Search

Select your language

MongoDB Shell

On this page

  * Prerequisites
  * Create the Atlas Search Index for Facet
  * Search the Collection
  * Continue Learning

This tutorial describes how to create an index with a facet definition on
string, date, and numeric fields in the `sample_mflix.movies` collection. It
shows how to run an Atlas Search query against those fields for results
grouped by values for the string field and by ranges for the date and numeric
fields, including the count for each of those groups. It takes you through the
following steps:

  1. Set up an Atlas Search index with facet definition on the `genres`, `released`, and `year` fields in the `sample_mflix.movies` collection.

  2. Run Atlas Search query against the `released` field in the `sample_mflix.movies` collection for results grouped by values for the `genres` field and by ranges for the `year` field.

## Prerequisites

To complete these tutorials, in addition to the prerequisites listed in the
Atlas Search Tutorials page, you must have an Atlas cluster running one of the
following versions:

  * MongoDB 4.4.11 or later

  * MongoDB 5.0.4 or later

  * MongoDB 6.0

## Create the Atlas Search Index for Facet

In this section, you will create an Atlas Search index on the `genres`,
`year`, and `released` fields in the `sample_mflix.movies` collection.

1

### Navigate to the Atlas Search page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

### Click Create Index.

3

### Select a Configuration Method and click Next.

  * For a guided experience, select Visual Editor.

  * To edit the raw index definition, select JSON Editor.

4

### Enter the Index Name, and set the Database and Collection.

  1. In the Index Name field, enter `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

  2. In the Database and Collection section, find the `sample_mflix` database, and select the `movies` collection.

5

### Specify an index definition.

The following index definition uses `lucene.standard` as the default analyzer
for both indexing and querying the fields and specifies the following for the
fields to index:

Field Name

|

Data Type  
  
|  
  
`genres`

|

How to Index String Fields For Faceted Search  
  
`year`

|

How to Index Numeric Values for Faceted Search  
  
`released`

|

How to Index Date Fields  
  
You can use the Visual Editor or the JSON Editor in the Atlas user interface
to create the index.

Visual Editor

JSON Editor

  1. Click Next.

  2. Click Refine Your Index.

  3. In the Index Configuration section, toggle to disable Dynamic Mapping.

  4. Click Add Field in the Field Mappings section and add the following fields by clicking Add after configuring the settings for each field in the Add Field Mapping window.

Field Name

|

Data Type Configuration  
  
|  
  
`genres`

|

Click the Data Type dropdown and select StringFacet.  
  
`year`

|

Click the Data Type dropdown and select NumberFacet. Use the default settings
for the `NumberFacet` properties.  
  
`released`

|

Click the Data Type dropdown and select Date.  
  
  5. Click Save Changes.

6

### Click Create Search Index.

7

### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

8

### Wait for the index to finish building.

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

## Search the Collection

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
examples in this section.

* * *

You can use facet in queries that use the `$search` and `$searchMeta` stages.
In this section, connect to your Atlas cluster and the run the sample query
against the `sample_mflix.movies` collection using the `$searchMeta` stage.
MongoDB recommends using the `$searchMeta` stage to retrieve metadata results
only.

MongoDB Shell

Compass

Go

Java (Sync)

Node.js

Python

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `sample_mflix` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_mflix  
      
  
MongoDB Shell

3

### Run an Atlas Search facet query that groups the genre and year fields into
buckets.

The following query searches for movies released near November 11, 1921. It
specifies a `pivot` distance from `origin` of approximately three months. It
requests metadata on the `genres` and `year` field. The query requests a count
of the:

  * Number of movies in each genre in the `genres` string array field

  * Number of movies in the years 1910 to 1939, inclusive

    
    
    db.movies.aggregate([  
      
      {  
        "$searchMeta": {  
          "facet": {  
            "operator": {  
              "near": {  
                "path": "released",  
                "origin": ISODate("1921-11-01T00:00:00.000+00:00"),  
                "pivot": 7776000000  
              }  
            },  
            "facets": {  
              "genresFacet": {  
                "type": "string",  
                "path": "genres"  
              },  
              "yearFacet" : {  
                "type" : "number",  
                "path" : "year",  
                "boundaries" : [1910,1920,1930,1940]  
              }  
            }  
          }  
        }  
      }  
    ])  
  
MongoDB Shell

The query returns the following results:

    
    
    {  
      
      "count" : {  
        "lowerBound" : NumberLong(23026)  
      },  
      "facet" : {  
        "genresFacet" : {  
          "buckets" : [  
            { "_id" : "Drama", "count" : NumberLong(13527) },  
            { "_id" : "Comedy", "count" : NumberLong(6922) },  
            { "_id" : "Romance", "count" : NumberLong(3615) },  
            { "_id" : "Crime", "count" : NumberLong(2649) },  
            { "_id" : "Thriller", "count" : NumberLong(2603) },  
            { "_id" : "Action", "count" : NumberLong(2505) },  
            { "_id" : "Documentary", "count" : NumberLong(2041) },  
            { "_id" : "Adventure", "count" : NumberLong(2016) },  
            { "_id" : "Horror", "count" : NumberLong(1662) },  
            { "_id" : "Biography", "count" : NumberLong(1373) }  
          ]  
        },  
        "yearFacet" : {  
          "buckets" : [  
            { "_id" : 1910, "count" : NumberLong(23) },  
            { "_id" : 1920, "count" : NumberLong(89) },  
            { "_id" : 1930, "count" : NumberLong(308) }  
          ]  
        }  
      }  
    }  
  
MongoDB Shell

The results show metadata results for two types of facet search. The
`genresFacet` document shows the number of movies in each genre and the
`yearFacet` document shows a count of the number of movies within the
boundaries:

  * `1910`, inclusive lower bound the `1910` bucket

  * `1920`, exclusive upper bound for the `1910` bucket and inclusive lower bound for the `1920` bucket

  * `1930`, exclusive upper bound for the `1920` bucket and inclusive lower bound for the `1930` bucket

## Continue Learning

To learn more about using facets in Atlas Search, take Unit 9 of the Intro To
MongoDB Course on MongoDB University. The 1.5 hour unit includes an overview
of Atlas Search and lessons on creating Atlas Search indexes, running
`$search` queries using compound operators, and grouping results using
`facet`.

← How to Run an Atlas Search Compound Geo JSON QueryHow to Run Partial Match
Atlas Search Queries →

