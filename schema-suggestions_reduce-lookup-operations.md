Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Reduce `$lookup` Operations

Share Feedback

On this page

  * Overview
  * Examples
  * Denormalization
  * Learn More

## Overview

`$lookup` operations join data from two collections in the same database based
on a specified field. `$lookup` operations can be useful when your data is
structured similarly to a relational database and you need to model large
hierarchical datasets. However, these operations can be slow and resource-
intensive because they need to read and perform logic on two collections
instead of a single collection.

If you frequently run `$lookup` operations, consider restructuring your schema
such that the your application can query a single collection to obtain all of
the information it needs. You can utilize MongoDB's flexible schema model with
embedded documents and arrays to capture relationships between data in a
single document structure. Use this denormalized model to take advantage of
MongoDB's rich documents and allow your application to retrieve and manipulate
related data in a single query.

## Examples

The following examples show two schema structures designed to reduce `$lookup`
operations:

  * Use Embedded Documents

  * Use Arrays

### Use Embedded Documents

Consider the following example where a grocery store tracks one-to-one
inventory and nutrition information in two separate collections. Each
inventory item corresponds to a unique nutrition facts item. The
`nutrition_id` field links the `inventory` collection to the `nutrition_facts`
collection, similar to a tabular database:

    
    
    // inventory collection  
      
      
    {  
       "name": "Pear",  
       "stock": 20,  
       "nutrition_id": 123, // reference to a nutrition_fact document  
       ...  
    }  
      
    {  
       "name": "Candy Bar",  
       "stock": 26,  
       "nutrition_id": 456,  
       ...  
    }  
      
    
    // nutrition_facts collection  
      
      
    {  
       "_id": 123,  
       "calories": 100,  
       "grams_sugar": 17,  
       "grams_protein": 1,  
       ...  
    }  
      
    {  
       "_id": 456,  
       "calories": 250,  
       "grams_sugar": 27,  
       "grams_protein": 4,  
       ...  
    }  
  
If an application requests the nutrition facts for an inventory item by
`name`, this schema structure requires a `$lookup` of the `nutrition_facts`
collection to find an entry that matches the inventory item's `nutrition_id`.

Instead, you can embed the nutrition information inside the `inventory`
collection:

    
    
    // inventory collection  
      
      
    {  
       "name": "Pear",  
       "stock": 20,  
       "nutrition_facts": {  
          "calories": 100,  
          "grams_sugar": 17,  
          "grams_protein": 1,  
          ...  
       }  
       ...  
    }  
      
    {  
       "name": "Candy Bar",  
       "stock": 26,  
       "nutrition_facts": {  
          "calories": 250,  
          "grams_sugar": 27,  
          "grams_protein": 4,  
          ...  
       }  
       ...  
    }  
  
This way, when you query for an item in `inventory`, the nutrition facts are
included in the result without the need for another query or a `$lookup`
operation. Consider embedding documents when data across collections has a
one-to-one relationship.

### Use Arrays

Consider the following example where documents in a baseball league's
`players` collection reference documents in a `teams` collection, similar to a
tabular database:

    
    
    // players collection  
      
      
    {  
       "team_id": 1, // reference to a team document  
       "name": "Nick",  
       "position": "Pitcher"  
       ...  
    }  
      
    {  
       "team_id": 1,  
       "name": "Anuj",  
       "position": "Shortstop"  
       ...  
    }  
      
    
    // teams collection  
      
      
    {  
       "_id": 1,  
       "name": "Danbury Dolphins"  
       ...  
    }  
  
If an application requests a list of players on a team, this schema structure
requires a `$lookup` of the `players` collection to find each player that
matches a `team_id`.

Instead, you can list the `players` in an array on the team document itself:

    
    
    // teams collection  
      
      
    {  
        "_id": 1,  
        "name": "Danbury Dolphins",  
        "players": [  
           {  
              "name": "Nick",  
              "position": "Pitcher"  
              ...  
           },  
           {  
              "name": "Anuj",  
              "position": "Shortstop"  
              ...  
           }  
        ]  
    }  
  
By using arrays to hold related data, an application can retrieve complete
`team` information, including that team's players, without `$lookup`
operations or indexes on other collections. In this case, using arrays is more
performant than storing the information in separate collections.

## Note

In the example above, the baseball teams have a set number of players and
there is no risk of arrays becoming exceedingly large.

#### Array Considerations

The performance cost of reading and writing to large arrays can outweigh the
benefit gained by avoiding `$lookup` operations. If your arrays are unbounded
or exceedingly large, those arrays may degrade read and write performance.

If you create an index on an array, each element in the array is indexed. If
you write to that array frequently, the performance cost of indexing or re-
indexing a potentially large array field may be significant.

## Tip

### See also:

## Denormalization

Denormalizing your schema is the process of duplicating fields or deriving new
fields from existing ones. Denormalization can improve read performance in a
variety of cases, such as:

  * A recurring query requires a few fields from a large document in another collection. You may choose to maintain a copy of those fields in an embedded document in the collection that the recurring query targets to avoid merging two distinct collections or performing frequent `$lookup` operations.

  * An average value of some field in a collection is frequently requested. You may choose to create a derived field in a separate collection that is updated as part of your writes and maintains a running average for that field.

While embedding documents or arrays without duplication is preferred for
grouping related data, denormalization can improve read performance when
separate collections must be maintained.

## Note

When you denormalize your schema, it becomes your responsibility to maintain
consistent duplicated data.

## Learn More

The best structure for your schema depends on your application context. The
following resources provide detailed information on data modeling and
additional example use cases for embedded documents and arrays:

### Data Models

  * To learn more about Data Modeling in MongoDB and the flexible schema model, see Data Modeling Introduction.

  * To learn more about the tradeoffs between embedded and normalized data models, see Data Model Design.

  * MongoDB also offers a free MongoDB University Course on Data Modeling: M320: Data Modeling.

#### MongoDB.live 2020 Data Modeling Presentations

To learn how to incorporate the flexible data model into your schema, see the
following presentations from **MongoDB.live 2020** :

  * Learn about entity relationships in MongoDB and examples of their implementations with Data Modeling with MongoDB.

  * Learn advanced data modeling design patterns you can incorporate into your schema with Advanced Schema Design Patterns.

### Arrays

To learn more about how to query arrays in MongoDB, see Query an Array.

### Design Patterns

To read about situations in which arrays work well, see the following design
patterns:

  * Use The Attribute Pattern for handling data with unique combinations of attributes, such as movie data where each movie is released in a subset of countries.

  * Use The Bucket Pattern for handling tightly grouped or sequential data, such as time span data.

  * Use The Polymorphic Pattern for handling differently shaped documents in the same collection, such as athlete records across several sports.

### Denormalized Schemas

To read about a situation in which duplicating data improves your schema, see
the following design pattern:

  * Use The Extended Reference Pattern to duplicate a frequently-read portion of data from large documents to smaller ones.

← Improve Your SchemaAvoid Unbounded Arrays →

