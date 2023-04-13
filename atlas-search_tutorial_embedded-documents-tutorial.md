Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run Atlas Search Queries Against Objects in Arrays

Select your language

MongoDB Shell

On this page

  * Create a Sample Collection and Load the Data
  * Create an Atlas Search Index
  * Run Atlas Search Queries Against Embedded Document Fields

This tutorial describes how to index and run queries against fields in
documents that are inside an array. This tutorial takes you through the
following steps:

  1. Create a sample collection named `schools` with embedded documents in your Atlas cluster.

  2. Set up an Atlas Search index with How to Index Fields in Arrays of Objects and Documents fields configured at the `teachers` and `teachers.classes` paths.

  3. Run Atlas Search queries that search the embedded documents in the the `schools` collection using the compound operator with the embeddedDocument and text operators.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites. For this tutorial, you don't need to upload
the sample data because you will create a new collection and load the
documents that you need to run the queries in this tutorial.

## Create a Sample Collection and Load the Data

Each document in the sample collection named `schools` contains the `name` and
`mascot` of the school, school teacher's `first` and `last` name, the
`classes` that each teacher teaches including the `subject` name and `grade`
level.

You must begin by creating a collection named `schools` in an existing or new
database on your Atlas cluster. After creating the collection, you must upload
the sample data into your collection. The steps in this section walk you
through creating a new database and collection, and loading the sample data
into your collection.

1

### Log in to Atlas and navigate to the Collections tab.

  1. Log in to your cluster.

  2. Click your cluster name.

  3. Click Collections.

2

### Create a new collection.

  1. Click Create Database to create a new database.

  2. Enter the database name and collection name.

    * In the Database Name field, specify `local_school_district`.

    * For the Collection Name field, specify `schools`.

3

### Load the following documents into the collection.

  1. Select the `schools` collection if it's not selected.

  2. Click Insert Document for each of the sample documents to add to the collection.

  3. Click the JSON view ({}) to replace the default document.

  4. Copy and paste the following sample documents, one at a time, and click Insert to add the documents, one at a time, to the collection.
    
        {  
      
      "_id": 0,  
      "name": "Springfield High",  
      "mascot": "Pumas",  
      "teachers": [{  
        "first": "Jane",  
        "last": "Smith",  
        "classes": [{  
          "subject": "art of science",  
          "grade": "12th"  
        },  
        {  
          "subject": "applied science and practical science",  
          "grade": "9th"  
        },  
        {  
          "subject": "remedial math",  
          "grade": "12th"  
        },  
        {  
          "subject": "science",  
          "grade": "10th"  
        }]  
      },  
      {  
        "first": "Bob",  
        "last": "Green",  
        "classes": [{  
          "subject": "science of art",  
          "grade": "11th"  
        },  
        {  
          "subject": "art art art",  
          "grade": "10th"  
        }]  
      }]  
    }  
      
        {  
      
      "_id": 1,  
      "name": "Evergreen High",  
      "mascot": "Jaguars",  
      "teachers": [{  
        "first": "Jane",  
        "last": "Earwhacker",  
        "classes": [{  
          "subject": "art",  
          "grade": "9th"  
        },  
        {  
          "subject": "science",  
          "grade": "12th"  
        }]  
      },  
      {  
        "first": "John",  
        "last": "Smith",  
        "classes": [{  
          "subject": "math",  
          "grade": "12th"  
        },  
        {  
          "subject": "art",  
          "grade": "10th"  
        }]  
      }]  
    }  
      
        {  
      
      "_id": 2,  
      "name": "Lincoln High",  
      "mascot": "Sharks",  
      "teachers": [{  
        "first": "Jane",  
        "last": "Smith",  
        "classes": [{  
          "subject": "science",  
          "grade": "9th"  
        },  
        {  
          "subject": "math",  
          "grade": "12th"  
        }]  
      },  
      {  
        "first": "John",  
        "last": "Redman",  
        "classes": [{  
          "subject": "art",  
          "grade": "12th"  
        }]  
      }]  
    }  
  

## Create an Atlas Search Index

In this section, you will create an Atlas Search index for the fields in the
embedded documents in the `local_school_district.schools` collection.

1

### Navigate to the Atlas Search page for your project.

  1. If it isn't already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it isn't already displayed, select your desired project from the Projects menu in the navigation bar.

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

  2. In the Database and Collection section, find the `local_school_district` database, and select the `schools` collection.

5

### Specify an index configuration that indexes embedded documents.

The following index definition specifies that documents in the arrays at the
`teachers` and `teachers.classes` paths must be indexed as How to Index Fields
in Arrays of Objects and Documents, and the fields inside the documents must
be dynamically indexed.

Visual Editor

JSON Editor

  1. Click Next.

  2. Click Refine Your Index.

  3. In the Field Mappings section, click Add Field.

  4. Select teachers from the Field Name dropdown.

  5. Click the Data Type dropdown and select EmbeddedDocuments.

  6. Toggle to enable Enable Dynamic Mapping if it isn't already enabled.

  7. Click Add.

  8. Click Add Embedded Field associated with the teachers field in the Field Mappings table.

  9. Select .classes under the teachers field from the Field Name dropdown.

  10. Click the Data Type dropdown and select EmbeddedDocuments.

  11. Toggle to enable Enable Dynamic Mapping if it isn't already enabled.

  12. Click Save.

  13. Click Save Changes.

6

### Click Create Search Index.

Atlas displays a modal window to let you know your index is building.

7

### Click the Close button and wait for the index to finish building.

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

## Run Atlas Search Queries Against Embedded Document Fields

You can run queries against the embedded document fields. This tutorial uses
embeddedDocument and text operators inside the compound operator in the
queries.

In this section, you will connect to your Atlas cluster and run the sample
queries using the operators against the fields in the `schools` collection.

* * *

➤ Use the **Select your language** drop-down menu on this page to set the
language of the examples in this section.

* * *

MongoDB Shell

Compass

Go

Java (Sync)

Node.js

Python

1

### Connect to your cluster using `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `local_school` database.

Run the following command at `mongosh` prompt:

    
    
    use local_school_district  
      
  
MongoDB Shell

HIDE OUTPUT

    
    
    switched to db local_school_district  
      
  
3

### Run the following Atlas Search queries against the `schools` collection.

The following queries search the documents inside the `teachers` array. The
queries use the following pipeline stages:

  * `$search` to search the collection.

  * `$project` to include the `_id` field and all the fields in the `teachers` array of documents, and add a field named `score` in the results.

Basic Search

Nested Array Search

The following query searches at the `teachers` path for teachers with the
first name `John` and specifies a preference for teachers with the last name
`Smith`.

    
    
    1| db.schools.aggregate({  
    |  
    2|   "$search": {  
    3|     "embeddedDocument": {  
    4|       "path": "teachers",  
    5|       "operator": {  
    6|         "compound": {  
    7|           "must": [{  
    8|             "text": {  
    9|               "path": "teachers.first",  
    10|               "query": "John"  
    11|             }  
    12|           }],  
    13|           "should":[{  
    14|             "text": {  
    15|               "path": "teachers.last",  
    16|               "query": "Smith"  
    17|             }  
    18|           }]  
    19|         }  
    20|       }  
    21|     }  
    22|   }  
    23| },  
    24| {  
    25|   "$project": {  
    26|     "_id": 1,  
    27|     "teachers": 1,  
    28|     "score": { $meta: "searchScore" }  
    29|   }  
    30| })  
  
MongoDB Shell

HIDE OUTPUT

    
    
    1| [  
    |  
    2|   {  
    3|     _id: 1,  
    4|     teachers: [  
    5|       {  
    6|         firstName: 'Jane',  
    7|         lastName: 'Earwhacker',  
    8|         classes: [  
    9|           { subject: 'art', grade: '9th' },  
    10|           { subject: 'science', grade: '12th' }  
    11|         ]  
    12|       },  
    13|       {  
    14|         firstName: 'John',  
    15|         lastName: 'Smith',  
    16|         classes: [  
    17|           { subject: 'math', grade: '12th' },  
    18|           { subject: 'art', grade: '10th' }  
    19|         ]  
    20|       }  
    21|     ],  
    22|     score: 0.7830756902694702  
    23|   },  
    24|   {  
    25|     _id: 2,  
    26|     teachers: [  
    27|       {  
    28|         firstName: 'Jane',  
    29|         lastName: 'Smith',  
    30|         classes: [  
    31|           { subject: 'science', grade: '9th' },  
    32|           { subject: 'math', grade: '12th' }  
    33|         ]  
    34|       },  
    35|       {  
    36|         firstName: 'John',  
    37|         lastName: 'Redman',  
    38|         classes: [ { subject: 'art', grade: '12th' } ]  
    39|       }  
    40|     ],  
    41|     score: 0.468008816242218  
    42|   }  
    43| ]  
  
The two documents in the results contain teachers with the first name `John`.
The document with `_id: 1` ranks higher because it contains a teacher with the
first name `John` who also has the last name `Smith`.

← How to Run Atlas Search Compound Queries with Weighted FieldsHow to Run
Atlas Search Queries with a Date Range Filter →

