Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run `$unionWith` with an Atlas Search `$search` Query

Share Feedback

On this page

  * Create the Atlas Search Indexes
  * Run `$unionWith` with `$search` to Search the Collections

Starting in v6.0, the MongoDB `$unionWith` aggregation stage supports
`$search` inside the `$unionWith` `pipeline` option. Using `$unionWith`, you
can combine `$search` results from multiple collections in the same database
in the result set.

This tutorial demonstrates how to run a `$unionWith` query with `$search`
against the `companies` and `inspections` collections in the `sample_training`
database. It takes you through the following steps:

  1. Set up an Atlas Search index with dynamic mappings for the `companies` and `inspections` collections in the `sample_training` database.

  2. Run `$unionWith` query with `$search` to perform a union of companies with `mobile` in their name from the `companies` collection with companies with same or similar business name in the `inspections` collection.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Note

To run a `$unionWith` query with `$search`, your cluster must run MongoDB v6.0
or higher.

## Create the Atlas Search Indexes

In this section, you will create an Atlas Search index named `default` on all
the fields in the `companies` collection in the `sample_training` database.
You will create another Atlas Search index named `default` on all the fields
in the `inspections` collection in the `sample_training` database. You must
perform the following steps for each collection.

1

### Navigate to the Atlas Search page for your project.

  1. If it isn't already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it isn't already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

### Create an index.

  * For your first index, click Create Search Index.

  * For subsequent indexes, click Create Index.

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

  2. In the Database and Collection section, find the `sample_training` database, and select the collection.

    * To create an index for the `companies` collection, select `companies`.

    * To create an index for the `inspections` collection, select `inspections`.

5

### Specify an index definition.

The following index definition dynamically indexes the fields of supported
types in the collection. You can use the Visual Editor or the JSON Editor in
the Atlas user interface to create the index.

Visual Editor

JSON Editor

  1. Click Next.

  2. Review the `"default"` index definition for the collection.

6

### Click Create Search Index.

7

### Close the You're All Set! Modal Window.

A modal window displays to let you know your index is building. Click the
Close button.

8

### Wait for the index to finish building.

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

## Run `$unionWith` with `$search` to Search the Collections

In this section, you will connect to your Atlas cluster and run the sample
query against the indexed collections in the `sample_training` database.

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Switch to the `sample_training` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_training  
      
  
HIDE OUTPUT

    
    
    switched to db sample_training  
      
  
3

### Run the following `$unionWith` with an Atlas Search `$search` query.

The following queries search both the `companies` and `inspections`
collections for the term `mobile` in the `name` and `business_name` fields
respectively. The query uses the following stages:

  * `$search` to search for companies that include `mobile` in the name.

  * `$unionWith` to do the following:

    * Use `$search` stage in the sub-pipeline to search for inspections of companies that include `mobile` in the name.

    * Perform a union of documents from the `companies` and documents from the `inspections` collections.

  * `$set` stage to add a new field named `source` that identifies the collection of the output documents.

  * `$limit` stage to limit the output to `3` results from each collection.

  * `$project` stage to:

    * Include only the specified fields in the results.

    * Add a field named `score`.

Basic Example

Facet Example

    
    
    db.companies.aggregate([  
      
    {  
      "$search": {  
        "text": {  
          "query": "Mobile",  
          "path": "name"  
        }  
      }  
    }, {  
      "$project": {  
        "score": {  
          "$meta": "searchScore"  
        },  
        "_id": 0,  
        "number_of_employees": 1,  
        "founded_year": 1,  
        "name": 1  
      }  
    }, {  
      "$set": {  
        "source": "companies"  
      }  
    }, {  
      "$limit": 3  
    }, {  
      "$unionWith": {  
        "coll": "inspections",  
        "pipeline": [  
          {  
            "$search": {  
              "text": {  
                "query": "Mobile",  
                "path": "business_name"  
              }  
            }  
          }, {  
            "$set": {  
              "source": "inspections"  
            }  
          }, {  
            "$project": {  
              "score": {  
                "$meta": "searchScore"  
              },  
              "source": 1,  
              "_id": 0,  
              "business_name": 1,  
              "address": 1  
            }  
          },  {  
            "$limit": 3  
          }, {  
            "$sort": {  
              "score": -1  
            }  
          }  
        ]  
      }  
    }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        name: 'XLR8 Mobile',  
        number_of_employees: 21,  
        founded_year: 2006,  
        score: 2.0815043449401855,  
        source: 'companies'  
      },  
      {  
        name: 'Pulse Mobile',  
        number_of_employees: null,  
        founded_year: null,  
        score: 2.0815043449401855,  
        source: 'companies'  
      },  
      {  
        name: 'T-Mobile',  
        number_of_employees: null,  
        founded_year: null,  
        score: 2.0815043449401855,  
        source: 'companies'  
      },  
      {  
        business_name: 'T. MOBILE',  
        address: { city: 'BROOKLYN', zip: 11209, street: '86TH ST', number: 440 },  
        score: 2.900916337966919,  
        source: 'inspections'  
      },  
      {  
        business_name: 'BOOST MOBILE',  
        address: { city: 'BRONX', zip: 10458, street: 'E FORDHAM RD', number: 261 },  
        score: 2.900916337966919,  
        source: 'inspections'  
      },  
      {  
        business_name: 'SPRING MOBILE',  
        address: {  
          city: 'SOUTH RICHMOND HILL',  
          zip: 11419,  
          street: 'LIBERTY AVE',  
          number: 12207  
        },  
        score: 2.900916337966919,  
        source: 'inspections'  
      }  
    ]  
  
← How to Run `$lookup` with an Atlas Search `$search` QueryHow to Build a
Search UI with Atlas App Services →

