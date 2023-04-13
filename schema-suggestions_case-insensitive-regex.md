Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Use Atlas Search for Full-Text Search Queries

Share Feedback

On this page

  * Avoid Inefficient Regex Matching
  * Example
  * Learn More

If your queries rely on inefficient regex matching, Atlas Search queries that
use the $search aggregation pipeline stage can significantly improve the
performance of text queries and offer more options for customizing query
parameters.

## Avoid Inefficient Regex Matching

If you frequently run case-insensitive regex queries (utilizing the `i`
option), we recommend Atlas Search queries that use the $search aggregation
pipeline stage. Alternatively, you can create a case-insensitive index to
support your queries. You can also specify a collation on an index to define
language-specific rules for string comparison, such as rules for lettercase
and accent marks. However, collation can cause some functionality loss
compared to Atlas Search queries. While a case-insensitive index improves
performance for case-insensitive queries, Atlas Search queries more
significiantly improve the performance of text queries and offer more options
for customizing query parameters.

## Example

Consider an `employees` collection with the following documents. This
collection has no indexes besides the default `_id` index:

    
    
    // employees collection  
      
      
    {  
      "_id": 1,  
      "first_name": "Hannah",  
      "last_name": "Simmons",  
      "dept": "Engineering"  
    },  
    {  
      "_id": 2,  
      "first_name": "Michael",  
      "last_name": "Hughes",  
      "dept": "Security"  
    },  
    {  
      "_id": 3,  
      "first_name": "Wendy",  
      "last_name": "Crawford",  
      "dept": "Human Resources"  
    },  
    {  
      "_id": 4,  
      "first_name": "MICHAEL",  
      "last_name": "FLORES",  
      "dept": "Sales"  
    }  
  
If your application frequently queries the `first_name` field, you may want to
run case-insensitive regex queries to more easily find matching names. Case-
insensitive regex also matches against differing data formats, as in the
example above where you have `first_names` of both "Michael" and "MICHAEL".
However, we recommend Atlas Search queries that use the $search aggregation
pipeline stage.

If a user searches for the string "michael", the application may run the
following query:

    
    
    db.employees.find( { first_name: { $regex: /michael/i } } )  
      
  
Since this query specifies the $regex option `i`, it is case-insensitive. The
query returns the following documents:

    
    
    { "_id" : 2, "first_name" : "Michael", "last_name" : "Hughes", "dept" : "Security" }  
      
    { "_id" : 4, "first_name" : "MICHAEL", "last_name" : "FLORES", "dept" : "Sales" }  
  
Although this query does return the expected documents, case-insensitive regex
queries with no index support are not very performant.

To improve performance, create an Atlas Search index. While you can create a
case-insensitive index on the `first_name` field, Atlas Search queries more
significantly improve the performance of text queries and offer more options
for customizing query parameters.

Regex Index

|

Atlas Search Index  
  
|  
      
    
    | db.employees.createIndex(  
      
      { first_name: 1 },  
      { collation: { locale: 'en', strength: 2 } }  
    )  
      
    
    | {  
      
      "mappings": {  
        "dynamic": true  
      }  
    }  
  
Collation can cause some functionality loss. When the `strength` field of an
index's `collation` document is `1` or `2`, the index is case-insensitive. For
a detailed description of the collation document and the different `strength`
values, see Collation Document.

For the application to use the case-insesitive index, you must also specify
the _same_ collation document from the index in the regex query. While you can
remove the `$regex` operator from the previous `find()` method and use the
newly created index, we recommend that you use an Atlas Search query that uses
the $search aggregation pipeline stage.

Regex Query

|

Atlas Search Query  
  
|  
      
    
    | db.employees.find( { first_name: "michael" } ).collation( { locale: 'en', strength: 2 } )  
      
      
    
    | db.employees.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "path": "first_name",  
            "query": "michael"  
          }  
        }  
      }  
    ])  
  
## Important

Do not use the $regex operator when using a case-insensitive index for your
query. The `$regex` implementation is not collation-aware and cannot utilize
case-insensitive indexes. Instead, we recommend Atlas Search queries that use
the $search aggregation pipeline stage.

## Learn More

  * To learn more about Atlas Search queries, see Create and Run Atlas Search Queries.

  * To learn more about case-insensitive indexes with illustrative examples, see Case Insensitive Indexes.

  * To learn more about regex queries in MongoDB, see $regex.

  * MongoDB University offers a free course on optimizing MongoDB Performance. To learn more, see M201: MongoDB Performance.

← Update $text Queries with Atlas Search for Improved Search PerformanceGet
Started with Atlas Search →

