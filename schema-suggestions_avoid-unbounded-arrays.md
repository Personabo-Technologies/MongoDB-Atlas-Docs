Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Avoid Unbounded Arrays

Share Feedback

On this page

  * Overview
  * Example
  * Learn More

## Overview

One of the benefits of MongoDB's rich schema model is the ability to store
arrays as document field values. Storing arrays as field values allows you to
model one-to-many or many-to-many relationships in a single document, instead
of across separate collections as you might in a relational database.

However, you should exercise caution if you are consistently adding elements
to arrays in your documents. If you do not limit the number of elements in an
array, your documents may grow to an unpredictable size. As an array continues
to grow, reading and building indexes on that array gradually decrease in
performance. A large, growing array can strain application resources and put
your documents at risk of exceeding the BSON Document Size limit.

Instead, consider bounding your arrays to improve performance and keep your
documents a manageable size.

## Example

Consider the following schema for a `publishers` collection:

    
    
    // publishers collection  
      
    {  
      "_id": "orielly"  
      "name": "O'Reilly Media",  
      "founded": 1980,  
      "location": "CA",  
      "books": [  
        {  
          "_id": 123456789,  
          "title": "MongoDB: The Definitive Guide",  
          "author": [ "Kristina Chodorow", "Mike Dirolf" ],  
          "published_date": ISODate("2010-09-24"),  
          "pages": 216,  
          "language": "English"  
        },  
        {  
          "_id": 234567890,  
          "title": "50 Tips and Tricks for MongoDB Developer",  
          "author": "Kristina Chodorow",  
          "published_date": ISODate("2011-05-06"),  
          "pages": 68,  
          "language": "English"  
        }  
      ]  
    }  
  
In this scenario, the `books` array is _unbounded_. Each new book released by
this publishing company adds a new sub-document to the `books` array. As
publishing companies continue to release books, the documents will eventually
grow very large and cause a disproportionate amount of memory strain on the
application.

To avoid mutable, unbounded arrays, separate the `publishers` collection into
two collections, one for `publishers` and one for `books`. Instead of
embedding the entire `book` document in the `publishers` document, include a
reference to the publisher inside of the book document:

    
    
    // publishers collection  
      
    {  
      "_id": "oreilly"  
      "name": "O'Reilly Media",  
      "founded": 1980,  
      "location": "CA"  
    }  
      
    
    // books collection  
      
    {  
      "_id": 123456789,  
      "title": "MongoDB: The Definitive Guide",  
      "author": [ "Kristina Chodorow", "Mike Dirolf" ],  
      "published_date": ISODate("2010-09-24"),  
      "pages": 216,  
      "language": "English",  
      "publisher_id": "oreilly"  
    }  
      
    {  
      "_id": 234567890,  
      "title": "50 Tips and Tricks for MongoDB Developer",  
      "author": "Kristina Chodorow",  
      "published_date": ISODate("2011-05-06"),  
      "pages": 68,  
      "language": "English",  
      "publisher_id": "oreilly"  
    }  
  
This updated schema removes the unbounded array in the `publishers` collection
and places a reference to the publisher in each book document using the
`publisher_id` field. This ensures that each document has a manageable size,
and there is no risk of a document field growing abnormally large.

### Document References May Require `$lookups`

This approach works especially well if your application loads the book and
publisher information separately. If your application requires the book and
information together, it needs to perform a `$lookup` operation to join the
data from the `publishers` and `books` collections. `$lookup` operations are
not very performant, but in this scenario may be worth the trade off to avoid
unbounded arrays.

## Learn More

  * To learn more about Data Modeling in MongoDB and the flexible schema model, see Data Modeling Introduction.

  * To learn how to model relationships with document references, see Model One-to-Many Relationships with Document References

  * To learn how to query arrays in MongoDB, see Query an Array.

  * MongoDB also offers a free MongoDB University Course on Data Modeling: M320: Data Modeling.

### MongoDB.live 2020 Presentations

To learn how to incorporate the flexible data model into your schema, see the
following presentations from **MongoDB.live 2020** :

  * Learn about entity relationships in MongoDB and examples of their implementations with Data Modeling with MongoDB.

  * Learn advanced data modeling design patterns you can incorporate into your schema with Advanced Schema Design Patterns.

← Reduce `$lookup` OperationsRemove Unnecessary Indexes →

