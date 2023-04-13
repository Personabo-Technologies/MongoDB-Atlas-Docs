Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `$merge`

Share Feedback

On this page

  * Permissions Required
  * Considerations
  * Syntax
  * Fields
  * Options
  * Resolving Duplicate Document IDs
  * Resolving Duplicate IDs in Atlas Data Federation
  * Remediating Duplicate IDs
  * Example
  * Merge Data Using `$merge`
  * Run `$merge` in the background

`$merge` writes the results of an aggregation pipeline to a temporary
collection on the Atlas cluster. Atlas Data Federation then runs `$merge`
locally on the Atlas cluster to **merge data in chunks** into the target
collection. In the event of a failure during a `$merge` operation, this
ensures that at least partial data is written to the target collection.

In Atlas Data Federation, `$merge` can:

  * Write data from any of the supported federated database instance stores.

  * Write to the same or different Atlas cluster, database, or collection within the same Atlas project.

To allow writes to an Atlas cluster, Atlas Data Federation introduces
alternate syntax for the required `into` field. Atlas Data Federation supports
all other fields as described for `$merge`.

To learn more, see `$merge` pipeline stage.

## Permissions Required

To use `$merge` to write to a collection on the Atlas cluster, you must be a
database user with the following privileges:

  * find and

  * insert

## Considerations

If the aggregation fails, Atlas Data Federation doesn't roll back any writes
that the `$merge` completed before the error occurred.

## Syntax

    
    
    {  
      
      "$merge": {  
        "into": {  
          "atlas": {  
            "projectId": "<atlas-project-ID>",  
            "clusterName": "<atlas-cluster-name>",  
            "db": "<atlas-database-name>",  
            "coll": "<atlas-collection-name>"  
          }  
        },  
        "on": "<identifier field>"|[ "<identifier field1>", ...],  
        "let": { <variables> },  
        "whenMatched": "replace|keepExisting|merge|fail|pipeline",  
        "whenNotMatched": "insert|discard|fail"  
      }  
    }  
  
## Fields

This section describes the alternate syntax that Atlas Data Federation
provides for the `into` field.

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`atlas`

|

object

|

Location to write the documents from the aggregation pipeline.

|

Required  
  
`clusterName`

|

string

|

Name of the Atlas cluster.

|

Required  
  
`coll`

|

string

|

Name of the collection on the Atlas cluster.

|

Required  
  
`db`

|

string

|

Name of the database on the Atlas cluster that contains the collection.

|

Required  
  
`projectId`

|

string

|

Unique identifier of the project that contains the Atlas cluster. This is the
ID of the project that contains your federated database instance. If omitted,
defaults to the ID of the project that contains your federated database
instance.

|

Optional  
  
To learn more about the other fields, `on`, `let`, `whenMatched`, and
`whenNotMatched`, see the MongoDB server documentation for `$merge`.

## Options

Option

|

Type

|

Description

|

Necessity  
  
|||  
  
`background`

|

boolean

|

Flag to run aggregation operations in the background. If omitted, defaults to
`false`. When set to `true`, Atlas Data Federation runs the queries in the
background.

    
    
    | { "background" : true }  
      
  
Use this option if you want to submit other new queries without waiting for
currently running queries to complete or disconnect your federated database
instance connection while the queries continue to run in the background.

Optional  
  
## Resolving Duplicate Document IDs

When writing documents from your archive or your data stores to your Atlas
cluster, your documents might have duplicate `_id` fields. This section
describes how Atlas Data Federation resolves duplicates and includes
recommendations for resolving duplicates in your aggregation pipeline.

### Resolving Duplicate IDs in Atlas Data Federation

To resolve duplicates, Atlas Data Federation:

  1. Writes documents to an Atlas collection `X` in the order it receives the documents until it encounters a duplicate.

  2. Writes the document with the duplicate `_id` field and all subsequent documents to a new Atlas collection `Y`.

  3. Runs the specified `$merge` stage to merge collection `Y` into collection `X`.

  4. Writes the resulting documents into the target collection on the specified Atlas cluster.

## Note

Atlas Data Federation only resolves duplicate values in the `_id` field. It
doesn't resolve duplicate values in other fields with unique indexes.

### Remediating Duplicate IDs

To remediate duplicate `_id` fields, you can:

  1. Include a `$sort` stage in your pipeline to specify the order in which Atlas Data Federation must process the resulting documents.

  2. Based on the order of documents flowing into the `$merge` stage, choose the value for the `whenMatched` and `whenNotMatched` options of the `$merge` stage carefully.

## Example

The following examples show how Atlas Data Federation resolves duplicates
during the `$merge` stage when `whenMatched` option is set to `keepExisting`
or `replace`. These examples use the following documents:

    
        {  
      
      "_id" : 1,  
      "state" : "FL"  
    },  
    {  
      "_id" : 1,  
      "state" : "NJ"  
    },  
    {  
      "_id" : 2,  
      "state" : "TX"  
    }  
  
keepExisting

replace

Suppose you run the following pipeline on the documents listed above:

    
        db.s3coll.aggregate([  
      
      {  
        "$sort": {  
          "_id": 1,  
          "state": 1,  
        }  
      },  
      {  
        "$merge": {  
          "into": {  
            "atlas": {  
              "clusterName": "clustername",  
              "db": "clusterdb",  
              "coll": "clustercoll"  
            }  
          },  
          "on": "_id",  
          "whenMatched": "keepExisting",  
          "whenNotMatched": "insert"  
        }  
      }  
    ])  
  
Atlas Data Federation writes the following data to two collections named `X`
and `Y`:

Collection X

Collection Y

    
        {  
      
      "_id" : 1,  
      "state" : "FL"  
    }  
  
Atlas Data Federation then merges documents from collection `Y` into
collection `X`. For `whenMatched: keepExisting` option in the pipeline, Atlas
Data Federation keeps the existing document with `_id: 1` in collection `X`.
Therefore, the result of the pipeline with duplicates contains the following
documents:

    
        {  
      
      "_id" : 1,  
      "state" : "FL"  
    },  
    {  
      "_id" : 2,  
      "state" : "TX"  
    }  
  
Atlas Data Federation then merges these documents into the target collection
on the specified Atlas cluster.

  3. Avoid using the `whenNotMatched: discard` option.

## Example

This example shows how Atlas Data Federation resolves duplicates when
`whenNotMatched` option is set to `discard` using the following documents:

    
        {  
      
      "_id" : 1,  
      "state" : "AZ"  
    },  
    {  
      "_id" : 1,  
      "state" : "CA"  
    },  
    {  
      "_id" : 2,  
      "state" : "NJ"  
    },  
    {  
      "_id" : 3,  
      "state" : "NY"  
    },  
    {  
      "_id" : 4,  
      "state" : "TX"  
    }  
  
Suppose you run the following pipeline on the documents listed above:

    
        db.archivecoll.aggregate([  
      
      {  
        "$sort": {  
          "_id": 1,  
          "state": 1,  
        }  
      },  
      {  
        "$merge": {  
          "into": {  
            "atlas": {  
              "clusterName": "clustername",  
              "db": "clusterdb",  
              "coll": "clustercoll"  
            }  
          },  
          "on": "_id",  
          "whenMatched": "replace",  
          "whenNotMatched": "discard"  
        }  
      }  
    ])  
  
Atlas Data Federation writes the following data to two collections named `X`
and `Y`:

Collection X

Collection Y

    
        {  
      
      "_id" : 1,  
      "state" : "AZ" // gets replaced  
    }  
  
Atlas Data Federation merges documents from collection `Y` into collection
`X`. For `whenMatched: replace` option in the pipeline, Atlas Data Federation
replaces the document with `_id: 1` in collection `X` with the document with
`_id: 1` in collection `Y`. For `whenNotMatched: discard` option in the
pipeline, Atlas Data Federation discards documents in collection `Y` that do
not match a document in collection `X`. Therefore, the result of the pipeline
with duplicates contains only the following document:

    
        {  
      
      "_id" : 1,  
      "state" : "CA"  
    }  
  
Atlas Data Federation then merges this document into the target collection on
the specified Atlas cluster.

## Example

### Merge Data Using `$merge`

The following example `$merge` syntax writes the results to a
`sampleDB.mySampleData` collection on the Atlas cluster named `myTestCluster`.
The example doesn't specify a project ID; the `$merge` stage uses the ID of
the project that contains your federated database instance.

## Example

    
    
    1| db.mySampleData.aggregate(  
    |  
    2|   [  
    3|     {  
    4|       "$merge": {  
    5|         "into": {  
    6|           "atlas": {  
    7|             "clusterName": "myTestCluster",  
    8|             "db": "sampleDB",  
    9|             "coll": "mySampleData"  
    10|           }  
    11|         },  
    12|         ...  
    13|       }  
    14|     }  
    15|   ]  
    16| )  
  
### Run `$merge` in the background

The following example `$merge` syntax writes the results to a
`sampleDB.mySampleData` collection on the Atlas cluster named `myTestCluster`
in the background. The example doesn't specify a project ID; the `$merge`
stage uses the ID of the project that contains your federated database
instance.

## Example

    
    
    1| db.mySampleData.aggregate(  
    |  
    2|   [  
    3|     {  
    4|       "$merge": {  
    5|         "into": {  
    6|           "atlas": {  
    7|             "clusterName": "myTestCluster",  
    8|             "db": "sampleDB",  
    9|             "coll": "mySampleData"  
    10|           }  
    11|         },  
    12|         ...  
    13|       }  
    14|     }  
    15|   ],  
    16|   { "background" : true }  
    17| )  
  
← `$lookup``$out` →

