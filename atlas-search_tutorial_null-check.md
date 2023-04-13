Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Check for Null and Non-Null Values with Atlas Search

Select your language

MongoDB Shell

On this page

  * Insert Sample Data
  * Create an Atlas Search Index with Dynamic Mapping
  * Check for `null` Values
  * Find All Non-`null` Values

This tutorial describes how to use Atlas Search queries to check your data for
`null` or non-`null` values. It takes you through the following steps:

  * Load sample documents with `null` values and missing fields into the `sample_mflix.users` collection.

  * Set up an Atlas Search index with dynamic mapping for the `sample_mflix.users` collection.

  * Run an Atlas Search query to find all documents with `null` values for the `password` field in the `sample_mflix.users` collection.

  * Run an Atlas Search query to find all documents that don't contain `null` values for the `password` field in the `sample_mflix.users` collection.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Insert Sample Data

In this section, you add sample documents that contain `null` values and
missing fields to the `sample_mflix.users` collection. These additional
documents allow you to successfully run the sample queries for `null` and
non-`null` values in this tutorial.

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Click your cluster's Browse Collections button.

3

### Insert documents into the `sample_mflix.users` collection.

  1. In the `sample_mflix` database, select the `users` collection.

  2. Click Insert Document.

  3. Click the JSON view ({}) to replace the default document.

  4. One at a time, copy and paste the following sample documents and click Insert to add the documents to the collection.
    
        { "name": "Andre Robinson", "email": "andre.robinson@gmail.com", "password": null }  
      
      
        { "name": "Laura Garcia", "email": "lgarcia@gmail.com" }  
      
  

## Create an Atlas Search Index with Dynamic Mapping

In this section, you create an Atlas Search index that uses dynamic mapping to
automatically index all the dynamically indexable fields in the
`sample_mflix.users` collection.

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

  2. In the Database and Collection section, find the `sample_mflix` database, and select the `users` collection.

5

### Specify an index definition.

You can create an Atlas Search index that uses dynamic mappings through the
Visual Editor or JSON Editor in the Atlas User Interface. The index definition
that you create dynamically indexes the fields of supported types in each
document in the `users` collection.

Visual Editor

JSON Editor

  1. Click Next.

  2. Review the `"default"` index definition for the `users` collection.

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

## Check for `null` Values

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
example on this page.

* * *

After setting up the Atlas Search index, you can connect to your Atlas cluster
and run queries against fields in the `sample_mflix.users` collection. The
following query uses the compound and wildcard operators to find all documents
that have a `password` field with a `null` value.

## Note

To successfully check for `null` values, the field that you are querying can't
have polymorphic data. For example, all other documents in the
`sample_mflix.users` collection have the `string` data type for the `password`
field.

MongoDB Shell

Compass

C#

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

### Run an Atlas Search query with the `compound` and `wildcard` operators on
the `users` collection.

The following query uses the `$search` pipeline stage to query the collection.
The query uses the following compound operator clauses:

  * `must` clause to find only documents that have the `password` field.

  * `mustNot` clause with the wildcard operator to exclude all documents that have any value in the `password` field.

    
    
    db.users.aggregate([  
      
        {  
            $search: {  
                "compound": {  
                    "must": {  
                        "exists": {  
                            "path": "password"  
                        }  
                    },  
                    "mustNot": {  
                        "wildcard": {  
                            "path": "password",  
                            "query": "*",  
                            "allowAnalyzedField": true  
                        }  
                    }  
                }  
            }  
        }  
    ])  
  
MongoDB Shell

This query returns the following results:

    
    
    1| {  
    |  
    2|    _id: ObjectId("63c84590975d5c7c8bf1ebed"),  
    3|    name: 'Andre Robinson',  
    4|    email: 'andre.robinson@gmail.com',  
    5|    password: null  
    6| }  
  
MongoDB Shell

Atlas Search returns one document with a `password` value that is `null`.
Atlas Search doesn't include documents that are missing the `password` field
because the query specifies that the `password` field must exist.

## Find All Non-`null` Values

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
example on this page.

* * *

After setting up the Atlas Search index, you can connect to your Atlas cluster
and run queries against fields in the `sample_mflix.users` collection. The
following query uses the compound and wildcard operators to find documents
that don't have a `null` value in the `password` field or don't have the
`password` field.

MongoDB Shell

Compass

C#

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

### Run an Atlas Search query with the `compound` and `wildcard` operators on
the `users` collection.

The following query searches only for users that do not have a `null` value in
the `password` field. The query includes the following pipeline stages:

  * `$search` pipeline stage to query the collection. The query uses the compound operator `should` clause to do the following:

    * Find all documents that don't have a `null` value in the `password` field using the wildcard operator.

    * Find documents that don't have the `password` field using the compound operator `mustNot` clause and replace their `score` with `2` using the `constant` option.

## Note

Atlas Search returns documents in order from highest score to lowest. In this
example, you alter the score for documents with a missing `password` field so
that they return first. Otherwise, these documents have a score of `0` and
return last. To learn more, see Scoring.

  * `$limit` stage to limit the output to `5` results.

  * `$project` stage to:

    * Exclude all fields except `name` and `password`.

    * Add a `score` field.

    
    
    db.users.aggregate([  
      
        {  
            $search: {  
                "compound": {  
                    "should": [{  
                            "wildcard": {  
                                "path": "password",  
                                "query": "*",  
                                "allowAnalyzedField": true  
                            }  
                        },  
                        {  
                            "compound": {  
                                "mustNot": {  
                                    "exists": {  
                                        "path": "password"  
                                    }  
                                },  
                                "score": { "constant": { "value": 2 } }  
                            }  
                        }  
                    ]  
                }  
            }  
        },   
        {  
        "$limit": 5  
        },  
        {  
            "$project": {  
                "_id": 0,   
                "name": 1,   
                "password": 1,  
                "score": { "$meta": "searchScore" }  
            }  
        }  
    ])  
  
MongoDB Shell

The query returns the following documents:

    
    
    1| { name: 'Laura Garcia', score: 2 },  
    |  
    2| {  
    3|   name: 'Ned Stark',  
    4|   password: '$2b$12$UREFwsRUoyF0CRqGNK0LzO0HM/jLhgUCNNIJ9RJAqMUQ74crlJ1Vu',  
    5|   score: 1  
    6| },  
    7| {  
    8|   name: 'Robert Baratheon',  
    9|   password: '$2b$12$yGqxLG9LZpXA2xVDhuPnSOZd.VURVkz7wgOLY3pnO0s7u2S1ZO32y',  
    10|   score: 1  
    11| },  
    12| {  
    13|   name: 'Jaime Lannister',  
    14|   password: '$2b$12$6vz7wiwO.EI5Rilvq1zUc./9480gb1uPtXcahDxIadgyC3PS8XCUK',  
    15|   score: 1  
    16| },  
    17| {  
    18|   name: 'Catelyn Stark',  
    19|   password: '$2b$12$fiaTH5Sh1zKNFX2i/FTEreWGjxoJxvmV7XL.qlfqCr8CwOxK.mZWS',  
    20|   score: 1  
    21| }  
  
MongoDB Shell

Atlas Search returns five documents with `password` values that are not
`null`. The first document listed in the results has a higher score because
the `constant` option alters the score for documents with a missing `password`
field.

← How to Build a Search UI with Atlas App ServicesHow to Paginate Query
Results →

