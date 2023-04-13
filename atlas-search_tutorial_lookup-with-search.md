Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run `$lookup` with an Atlas Search `$search` Query

Share Feedback

On this page

  * Create the Atlas Search Index
  * Run `$lookup` with `$search` to Search the Collections

Starting in v6.0, the MongoDB `$lookup` aggregation stage supports `$search`
inside the `$lookup` `pipeline` option. Using `$lookup`, you can join multiple
collections in the same database at query-time and run a `$search` query to
further narrow down your search.

## Note

`$lookup` queries are not very performant because Atlas Search does a full
document lookup on the database for each document in the collection. To learn
more, see Reduce `$lookup` Operations.

This tutorial demonstrates how to run a `$lookup` query with `$search` against
the `accounts` and `customers` collections in the `sample_analytics` database.
It takes you through the following steps:

  1. Set up an Atlas Search index with dynamic mapping for the `accounts` collection in the `sample_analytics` database.

  2. Run `$lookup` query with `$search` to find customers from the `customers` collections whose accounts have purchased both `CurrencyService` and `InvestmentStock` products in the `accounts` collection.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Note

To run `$lookup` query with `$search`, your cluster must run MongoDB v6.0 or
later. If not, Atlas Search displays the following error message:

    
    
    $_internalSearchMongotRemote is not allowed within a $lookup's sub-pipeline.  
      
  
To learn more, see Upgrade Major MongoDB Version for a Cluster.

## Create the Atlas Search Index

Create an Atlas Search index named `default` on all the fields in the
`sample_analytics.accounts` collection.

1

### Navigate to the Atlas Search page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

### Create an Atlas Search index.

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

  2. In the Database and Collection section, find the `sample_analytics` database, and select the `accounts` collection.

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

## Run `$lookup` with `$search` to Search the Collections

Connect to your Atlas cluster and run the sample query against the indexed
collections in the `sample_analytics` database.

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Switch to the `sample_analytics` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_analytics  
      
  
HIDE OUTPUT

    
    
    switched to db sample_analytics  
      
  
3

### Run the following `$lookup` with Atlas Search `$search` query.

The following query uses the following stages:

  * `$lookup` to do the following:

    * Join `customers` and `accounts` collections in the `sample_analytics` database based on the account ID of the customers and return the matching documents from the `accounts` collection in an array field named `purchases`.

    * Use `$search` stage in the sub-pipeline to search for customer accounts that `must` have purchased both `CurrencyService` and `InvestmentStock` with preference for an order limit between `5000` to `10000`.

  * `$limit` stage to limit the output to `5` results.

  * `$project` stage to exclude the specified fields in the results.

    
    
    db.customers.aggregate([  
      
      {  
        $lookup:{  
          "from": "accounts",  
          "localField": "accounts",  
          "foreignField": "account_id",  
          "as": "purchases",  
          "pipeline": [{  
            "$search": {  
              "compound": {  
                "must": [{  
                  "queryString": {  
                    "defaultPath": "products",  
                    "query": "products: (CurrencyService AND InvestmentStock)"  
                  }  
                }],  
                "should": [{  
                  "range": {  
                    "path": "limit",  
                    "gte": 5000,  
                    "lte": 10000  
                  }  
                }]  
              }  
            }  
          },{  
            "$project": {  
              "_id": 0  
            }  
          }]  
        }  
      },{  
        "$limit": 5  
      },{  
        "$project": {  
          "_id": 0,  
          "address": 0,  
          "birthdate": 0,  
          "username": 0,  
          "tier_and_details": 0  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        name: 'Elizabeth Ray',  
        email: 'arroyocolton@gmail.com',  
        active: true,  
        accounts: [ 371138, 324287, 276528, 332179, 422649, 387979 ],  
        purchases: [  
          {  
            account_id: 422649,  
            limit: 10000,  
            products: [ 'CurrencyService', 'InvestmentStock' ]  
          },  
          {  
            account_id: 324287,  
            limit: 10000,  
            products: [  
              'Commodity',  
              'CurrencyService',  
              'Derivatives',  
              'InvestmentStock'  
            ]  
          },  
          {  
            account_id: 332179,  
            limit: 10000,  
            products: [  
              'Commodity',  
              'CurrencyService',  
              'InvestmentFund',  
              'Brokerage',  
              'InvestmentStock'  
            ]  
          }  
        ]  
      },  
      {  
        name: 'Lindsay Cowan',  
        email: 'cooperalexis@hotmail.com',  
        accounts: [ 116508 ],  
        purchases: []  
      },  
      {  
        name: 'Katherine David',  
        email: 'timothy78@hotmail.com',  
        accounts: [ 462501, 228290, 968786, 515844, 377292 ],  
        purchases: [  
          {  
            account_id: 228290,  
            limit: 10000,  
            products: [  
              'CurrencyService',  
              'InvestmentStock',  
              'InvestmentFund',  
              'Brokerage'  
            ]  
          },  
          {  
            account_id: 515844,  
            limit: 10000,  
            products: [  
              'Commodity',  
              'CurrencyService',  
              'InvestmentFund',  
              'Brokerage',  
              'InvestmentStock'  
            ]  
          }  
        ]  
      },  
      {  
        name: 'Leslie Martinez',  
        email: 'tcrawford@gmail.com',  
        accounts: [ 170945, 951849 ],  
        purchases: []  
      },  
      {  
        name: 'Brad Cardenas',  
        email: 'dustin37@yahoo.com',  
        accounts: [ 721914, 817222, 973067, 260799, 87389 ],  
        purchases: [  
          {  
            account_id: 87389,  
            limit: 10000,  
            products: [ 'CurrencyService', 'InvestmentStock' ]  
          },  
          {  
            account_id: 260799,  
            limit: 10000,  
            products: [  
              'Brokerage',  
              'InvestmentStock',  
              'Commodity',  
              'CurrencyService'  
            ]  
          }  
        ]  
      }  
    ]  
  
← How to Run Atlas Search Queries Using Materialized ViewsHow to Run
`$unionWith` with an Atlas Search `$search` Query →

