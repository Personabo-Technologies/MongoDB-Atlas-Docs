Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Paginate Query Results

Share Feedback

On this page

  * Create the Atlas Search Index With Dynamic Mapping
  * Run a Query and Paginate the Results

## Important

The procedures in this tutorial might not be sufficient to optimize search
query performance for all use cases. To provide feedback on your use case, use
the MongoDB Feedback Engine.

Atlas Search queries might return many results. To make navigating results
easier, you can use pagination to divide results into discrete pages. You can
use the following aggregation pipeline stages to paginate your query results:

  1. `$skip` bypasses the specified number of documents that pass into the stage and passes the remaining documents to the next stage in the pipeline.

  2. `$limit` restricts the number of documents passed to the next stage in the pipeline.

You can extend this method to your applications so that a Next Page button
skips past the first ten results and shows the next ten results from that
point.

You can also use the `SEARCH_META` Aggregation Variable to return the total
number of search results. You can use this information in your applications to
show the total number of search results, or the number of pages available to
your application user.

This tutorial takes you through the following steps:

  1. Set up an Atlas Search index with dynamic mapping for the `sample_mflix.movies` collection.

  2. Run an Atlas Search query using the following:

    * `$skip` and `$limit` after the `$search` stage to paginate the results.

    * `SEARCH_META` Aggregation Variable to return the total number of search results.

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

## Run a Query and Paginate the Results

In this section, we run Atlas Search queries using the following:

  * `$skip` and `$limit` after the `$search` stage to paginate the results.

  * `SEARCH_META` Aggregation Variable to return the total number of search results in addition to paginating the results.

You can run one or all of the following queries against the collection using
the same index definition.

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `sample_mflix` database.

Run the following command in the `mongosh` prompt:

    
    
    use sample_mflix  
      
  
3

### Run an Atlas Search query against the `movies` collection.

You can run one or all of the following query examples against the collection
using the same index definition.

Paginate Results

Return Total and Paginate Results

The following query uses `$skip` and `$limit` after the `$search` stage to
paginate the results. It skips past the first ten results and shows the next
ten results from that point.

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "text": {  
            "query": "tom hanks",  
            "path": "cast"  
          }  
        }  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1,  
          "cast": 1  
        }  
      },  
      {  
        "$skip": 10  
      },  
      {  
        "$limit": 10  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        title: 'Toy Story',  
        cast: [ 'Tom Hanks', 'Tim Allen', 'Don Rickles', 'Jim Varney' ]  
      },  
      {  
        title: 'Toy Story 2',  
        cast: [ 'Tom Hanks', 'Tim Allen', 'Joan Cusack', 'Kelsey Grammer' ]  
      },  
      {  
        cast: [ 'Tom Hanks', 'Nick Searcy', 'Lane Smith', 'David Andrews' ],  
        title: 'From the Earth to the Moon'  
      },  
      {  
        title: "You've Got Mail",  
        cast: [ 'Tom Hanks', 'Meg Ryan', 'Greg Kinnear', 'Parker Posey' ]  
      },  
      {  
        cast: [  
          'Tom Hanks',  
          'Stephen Ambrose',  
          'Russ Meyer',  
          'Walter Rosenblum'  
        ],  
        title: 'Shooting War'  
      },  
      {  
        title: 'Catch Me If You Can',  
        cast: [  
          'Leonardo DiCaprio',  
          'Tom Hanks',  
          'Christopher Walken',  
          'Martin Sheen'  
        ]  
      },  
      {  
        title: 'The Polar Express',  
        cast: [ 'Tom Hanks', 'Leslie Zemeckis', 'Eddie Deezen', 'Nona Gaye' ]  
      },  
      {  
        cast: [ 'Tom Hanks', 'Audrey Tautou', 'Ian McKellen', 'Jean Reno' ],  
        title: 'The Da Vinci Code'  
      },  
      {  
        cast: [ 'Tom Hanks', 'Tim Allen', 'Joan Cusack', 'Ned Beatty' ],  
        title: 'Toy Story 3'  
      },  
      {  
        cast: [ 'Tom Hanks', 'Thomas Horn', 'Sandra Bullock', 'Zoe Caldwell' ],  
        title: 'Extremely Loud & Incredibly Close'  
      }  
    ]  
  
← How to Check for Null and Non-Null Values with Atlas SearchCreate and Manage
Atlas Search Indexes →

