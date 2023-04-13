Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Run Atlas Search Queries

Share Feedback

On this page

  * Run Atlas Search Queries in the Search Tester
  * Limitations
  * Prerequisites
  * Search Your Collection
  * View, Edit, or Copy Query Syntax
  * Run Atlas Search Queries in Compass, Drivers and `mongosh`

## Run Atlas Search Queries in the Search Tester

The Search Tester feature in the Search tab allows you to:

  * Enter the term to search in the collection.

  * Run a `$search` query. By default, the Search Tester uses a simple wildcard query.

  * View your Atlas Search query syntax, which you can then run in `mongosh` or MongoDB Compass.

The Search Tester returns the top 10 documents sorted based on relevance
score.

### Limitations

The Search Tester does not support faceted searches and the `$searchMeta`
aggregation pipeline stage.

### Prerequisites

To use the Search Tester in the Atlas UI, you must have the following:

  * An Atlas cluster running MongoDB version 4.2 or higher.

  * Atlas Search index on your collection in the Atlas cluster.

### Search Your Collection

1

Click the cluster name to view cluster details and select Search tab.

2

On the index you'd like to query, click the Query button on the righthand side
of the card.

3

#### Search the collection.

1

##### Enter the term to search in the search box.

2

##### Click Search to search the collection.

### View, Edit, or Copy Query Syntax

1

Click Edit $search Query to view your query syntax in JSON format.

2

#### Edit or copy your query syntax.

You can edit or copy the query syntax in JSON format.

1

##### Edit Query Syntax

You can update the `$search` query in the Search Editor and test it by
clicking the Search button.

## Important

When you finish editing your query, be sure to copy it. Once you click Close
Search Editor, the Atlas UI discards your changes.

2

##### Copy Query Syntax

Click __to copy the query syntax in JSON format to your clipboard. You can run
the copied query in your `mongosh` or MongoDB Compass after connecting to your
Atlas cluster.

3

#### Click Close Search Editor to exit the Edit $search Query modal.

## Note

The Atlas UI discards your changes when you exit the Search Tester Editor.

## Run Atlas Search Queries in Compass, Drivers and `mongosh`

To run a Atlas Search query, you must have the following:

  * An Atlas cluster running MongoDB version 4.2 or higher.

  * Atlas Search index on your collection in the Atlas cluster.

  * A connection to the client you want to use to run the query.

The Step 2: Run Atlas Search Queries page demonstrates how to connect to your
Atlas cluster and run `$search` queries against the `sample_mflix.movies`
collection using the following clients. To learn more, select a client using
the **Select your language** drop-down menu on the Step 2: Run Atlas Search
Queries page.

Client

|

Steps  
  
|  
  
MongoDB Compass

|

  1. Install and see Connect via Compass to connect to your Atlas cluster using MongoDB Compass.

  2. In the MongoDB Compass Aggregations tab, manually enter your aggregation pipeline.

To learn more, see Aggregation Pipeline Builder.  
  
Drivers

|

  1. Install any one of the following drivers:

    * C

    * C#/.NET

    * C++

    * Go

    * Java

    * Node.js

    * PHP

    * Python

    * Ruby

    * Rust

    * Scala

    * Swift

  2. See Connect via Your Application to connect to your Atlas cluster using the installed driver.

  3. Define and run an aggregation pipeline in your code editor.

To learn more about running `$search` queries using these drivers, see Step 2:
Run Atlas Search Queries. Each example in the Step 2: Run Atlas Search Queries
page performs the following:

  * Creates a connection to your Atlas cluster with the `MongoClient`.

  * Defines a pipeline.

  * Runs the pipeline.

  * Prints the query result.

  
  
MongoDB Shell

|

  1. Install and see Connect via `mongosh` to connect to your Atlas cluster using the MongoDB Shell.

  2. Define and run an Atlas Search query.

To learn more about running `$search` queries using `mongosh`, see Step 2: Run
Atlas Search Queries.  
  
← Count Atlas Search ResultsTroubleshoot Atlas Search Errors →

