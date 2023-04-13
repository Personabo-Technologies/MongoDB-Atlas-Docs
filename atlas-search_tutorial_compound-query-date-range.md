Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run Atlas Search Queries with a Date Range Filter

Share Feedback

On this page

  * Create the Atlas Search Index With Dynamic Mapping
  * Run a Compound Query

This tutorial describes how to create an index with dynamic mapping on the
`sample_mflix.movies` collection. It shows how to run compound queries against
the `released` field using the range and near operators. It takes you through
the following steps:

  1. Set up an Atlas Search index with dynamic mapping for the `sample_mflix.movies` collection.

  2. Run Atlas Search compound queries against the `released` field in the `sample_mflix.movies` collection.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Create the Atlas Search Index With Dynamic Mapping

In this section, we create an Atlas Search index that uses dynamic mapping to
index the fields in the `sample_mflix.movies` collection.

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

You can create an Atlas Search index that uses dynamic mappings through the
Visual Editor or JSON Editor in the Atlas User Interface. The following index
definition dynamically indexes the fields of supported types in the `movies`
collection.

#### Visual Editor

  1. Click Next.

  2. Review the `"default"` index definition for the `movies` collection.

#### JSON Editor

  1. Click Next.

  2. Review the index definition.

Your index definition should look similar to the following:

    
        {  
      
      "mappings": {  
        "dynamic": true  
      }  
    }  
  
The above index definition dynamically indexes the fields of supported types
in each document in the `movies` collection.

  3. Click Next.

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

## Run a Compound Query

You can use the compound operator to combine two or more operators and clauses
into a single query. This tutorial uses the compound operator clauses to
search for movies in the specified date range. In this section, connect to
your Atlas cluster and run the sample queries using the compound operator
against the `released` field in the `sample_mflix.movies` collection.

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `sample_mflix` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_mflix  
      
  
3

### Run the following Atlas Search queries with the `compound` operator on the
`movies` collection.

The following examples use the `compound` operator with subqueries to search
for movies between the years `2010` to `2015`. The query uses the following
clauses:

  * A `must` clause to search for movies released between `2015-01-01` and `2015-12-31`

  * A `should` clause to specify preference for movies released near `2012-07-01`, with a pivot distance of 1 month

The example queries include a `$limit` stage to limit the output to 6 results
and a `$project` stage to:

  * Exclude all fields except `title`, `released`, and `genres` fields

  * Add a field named `score`

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
           "compound": {  
             "must": [{  
               "range": {  
                 "path": "released",  
                 "gt": ISODate("2015-01-01T00:00:00.000Z"),  
                 "lt": ISODate("2015-12-31T00:00:00.000Z")  
               }  
             }],  
             "should": [{  
               "near": {  
                 "path": "released",  
                 "origin": ISODate("2015-07-01T00:00:00.000+00:00"),  
                 "pivot": 2629800000  
               }  
             }]  
           }  
         }  
       },  
       {  
         "$limit": 6  
       },  
       {  
         "$project": {  
           "_id": 0,  
           "title": 1,  
           "released": 1,  
           "genres": 1,  
           "score": { "$meta": "searchScore" }  
         }  
       }  
     ])  
  
Atlas Search returns the following results:

    
    
    [  
      
      {  
        "genres": [ "Action", "Adventure", "Sci-Fi" ],  
        "title": "Terminator Genisys",  
        "released": ISODate("2015-07-01T00:00:00.000Z"),  
        "score": 2  
      },  
      {  
        "genres": [ "Comedy", "Drama", "Music" ],  
        "title": "Magic Mike XXL",  
        "released": ISODate("2015-07-01T00:00:00.000Z"),  
        "score": 2  
      },  
      {  
        "genres": [ "Documentary", "Biography", "Drama" ],  
        "title": "Mala Mala",  
        "released": ISODate("2015-07-01T00:00:00.000Z"),  
        "score": 2  
      },  
      {  
        "genres": [ "Comedy", "Drama" ],  
        "title": "Home Care",  
        "released": ISODate("2015-07-01T00:00:00.000Z"),  
        "score": 2  
      },  
      {  
        "genres": [ "Documentary", "News" ],  
        "title": "Bitcoin: The End of Money as We Know It",  
        "released": ISODate("2015-07-01T00:00:00.000Z"),  
        "score": 2  
      },  
      {  
        "genres": [ "Drama", "Mystery", "Sci-Fi" ],  
        "title": "Pig",  
        "released": ISODate("2015-07-02T00:00:00.000Z"),  
        "score": 1.9681909084320068  
      }  
    ]  
  
For the query, the top results are in the month of July because the `should`
clause specified a preference for movies near July.

The following example uses the `compound` operator with subqueries, `$limit`
stage, and the `$project` stages to perform the same search as the previous
query. In addition to the `must` and `should` clauses, the query also includes
a `mustNot` clause to specify that movies in the `documentary` genre must not
be included in the results.

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
           "compound": {  
             "must": [{  
               "range": {  
                 "path": "released",  
                 "gt": ISODate("2015-01-01T00:00:00.000Z"),  
                 "lt": ISODate("2015-12-31T00:00:00.000Z")  
               }  
             }],  
             "should": [{  
               "near": {  
                 "path": "released",  
                 "origin": ISODate("2015-07-01T00:00:00.000+00:00"),  
                 "pivot": 2629800000  
               }  
             }],  
             "mustNot": [{  
               "text": {  
                 "query": "documentary",  
                 "path": "genres"  
               }  
             }]  
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
           "genres": 1,  
           "score": { "$meta": "searchScore" }  
         }  
       }  
     ])  
  
Atlas Search returns the following results:

    
    
    [  
      
      {  
        "genres": [ "Action", "Adventure", "Sci-Fi" ],  
        "title": "Terminator Genisys",  
        "released": ISODate("2015-07-01T00:00:00.000Z"),  
        "score": 2  
      },  
      {  
        "genres": [ "Comedy", "Drama", "Music" ],  
        "title": "Magic Mike XXL",  
        "released": ISODate("2015-07-01T00:00:00.000Z"),  
        "score": 2  
      },  
      {  
        "genres": [ "Comedy", "Drama" ],  
        "title": "Home Care",  
        "released": ISODate("2015-07-01T00:00:00.000Z"),  
        "score": 2  
      },  
      {  
        "genres": [ "Drama", "Mystery", "Sci-Fi" ],  
        "title": "Pig",  
        "released": ISODate("2015-07-02T00:00:00.000Z"),  
        "score": 1.9681909084320068  
      },  
      {  
        "genres": [ "Drama", "History", "Romance" ],  
        "title": "Gold Coast",  
        "released": ISODate("2015-07-02T00:00:00.000Z"),  
        "score": 1.9681909084320068  
      },  
      {  
        "genres": [ "Animation", "Family" ],  
        "title": "Zarafa",  
        "released": ISODate("2015-07-03T00:00:00.000Z"),  
        "score": 1.9383430480957031  
      }  
    ]  
  
For the query, the top results are in the month of July because the `should`
clause specified a preference for movies near July.

← How to Run Atlas Search Queries Against Objects in ArraysHow to Run an Atlas
Search Compound Geo JSON Query →

