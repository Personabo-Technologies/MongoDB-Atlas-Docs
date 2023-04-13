Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `$lookup`

Share Feedback

On this page

  * Syntax
  * `from` Field Object
  * Examples
  * Basic Example
  * Nested Example

The MongoDB server $lookup performs a left outer join of one unsharded
collection to another unsharded collection in the same database. Lookups are
useful as they allow you to filter in documents from the "joined" collection
for processing.

In federated database instance, you can use `$lookup` to join sharded and
unsharded collections from the same database or different databases from
Atlas, AWS S3, and HTTP or HTTPS data stores.

## Note

For sharded collections, `$lookup` is only available on Atlas clusters running
MongoDB 5.1 and later.

## Syntax

The `$lookup` syntax is described in the MongoDB server manual.

In Data Federation, the `from` field in `$lookup` has the following alternate
syntax. This allows you to specify an object that contains an optional
database name and a required collection name:

Equality Match

Conditions and Sub-Queries

    
    
    {  
      
      $lookup: {  
        localField: "<fieldName>",  
        from: <collection-to-join>|{db: <db>, coll: <collection-to-join>},  
        foreignField: "<fieldName>",  
        as: "<output-array-field>",  
      }  
    }  
  
## `from` Field Object

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`db`

|

string

|

The database name.

If you specify a database name, Data Federation reads data from the collection
in the specified database. If you specify a database name that differs from
the database upon which the command is operating, all nested $lookup stages
**must** also specify this database name.

If you don't specify a database name within a $lookup stage, collections in
the stage inherit the database name specified in the closest parent $lookup
stage if it exists, or the name of the database upon which the command is
operating.

|

Conditional  
  
`coll`

|

string

|

The collection name.

|

Required  
  
## Examples

Suppose there are three databases named `sourceDB1`, `sourceDB2`, and
`sourceDB3` with the following collections:

sourceDB1

sourceDB2

sourceDB3

    
    
    db.orders.insertMany([  
      
      { "_id" : 1, "item" : "almonds", "price" : 12, "quantity" : 2 },  
      { "_id" : 2, "item" : "pecans", "price" : 20, "quantity" : 1 },  
      { "_id" : 3  }  
    ])  
  
The following examples use the $lookup aggregation stage to join documents
from one collection with the documents from the collection in the other
databases.

### Basic Example

The following aggregation operation on the `sourceDB1.orders` collection joins
the documents from the `orders` collection with the documents from the
`sourceDB2.catalog` collection using the `item` field from the `orders`
collection and the `sku` field from the `catalog` collection:

    
    
    db.getSiblingDb("sourceDB1").orders.aggregate(  
      
      {  
        $lookup: {  
          from: { db: "sourceDB2", coll: "catalog" },  
          localField: "item",  
          foreignField: "sku",  
          as: "inventory_docs"  
        }  
      }  
    )  
  
### Nested Example

The following aggregation operation on the `sourceDB1.orders` collection joins
the documents from the `orders` collection with the documents from the
`sourceDB2.catalog` collection and the documents from the
`sourceDB3.warehouses` collection using the `item` field from the `orders`
collection, the `sku` field from the `catalog` collection, and the
`stock_item` and `instock` fields from the `warehouses` collection:

    
    
    db.getSiblingDb(“sourceDB1”).orders.aggregate(  
      
      [  
        {  
          $lookup: {  
            from: db: "sourceDB2", coll: "catalog",  
            let: { "order_sku": "$item" },  
            pipeline: [  
              {  
                $match: {  
                  $expr: {  
                    $eq: ["$sku", "$$order_sku"]  
                  }  
                }  
              },  
              {  
                $lookup: {  
                  from: db: "sourceDB3", coll: "warehouses",  
                  pipeline: [  
                    {  
                      $match: {  
                        $expr:{  
                          $eq : ["$stock_item", "$$order_sku"]  
                        }  
                      }  
                    },  
                    {  
                      $project : { "instock": 1, "_id": 0}  
                    }  
                  ],  
                  as: "wh"  
                }  
              },  
              { "$unwind": "$wh" },  
              {  
                $project : { "description": 1, "instock": "$wh.instock", "_id": 0}  
              }  
            ],  
            as: "inventory"  
          },  
        },  
      ]  
    )  
  
← `$collStats``$merge` →

