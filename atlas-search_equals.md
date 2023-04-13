Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# equals

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Behavior
  * Examples

## Definition

`equals`

    

The `equals` operator checks whether a field matches a value you specify.
`equals` supports querying the following data types:

  * boolean

  * objectId

  * number, including `int32`, `int64`, and `double`

  * date

You can use the `equals` operator to query booleans, objectIds, numbers, and
dates in arrays. If at least one element in the array matches the "value"
field in the `equals` operator, Atlas Search adds the document to the result
set.

## Note

The `equals` operator supports numbers up to 15 decimal digits. Additional
decimal digits in documents or queries can cause precision issues or query
inaccuracy.

## Syntax

`equals` has the following syntax:

    
    
    {  
      
       $search: {  
          "index": <index name>, // optional, defaults to "default"  
          "equals": {  
             "path": "<field-to-search>",  
             "value": <boolean-value>|<objectId>|<number>|<date>,  
             "score": <score-options>  
          }  
       }  
    }  
  
## Options

`equals` uses the following terms to construct a query:

Field

|

Type

|

Description

|

Required?  
  
|||  
  
`path`

|

string

|

Indexed field to search.

|

yes  
  
`value`

|

boolean, objectId, number, or date

|

Value to query for.

|

yes  
  
`score`

|

object

|

Score assigned to matching search term results. Use one of the following
options to modify the score:

  * `boost`: multiply the result score by the given number.

  * `constant`: replace the result score with the given number.

For information on using `score` in your query, see Customize and Normalize
the Score in Results.

|

no  
  
## Behavior

`equals` uses constant scoring. Each matching document receives a score of `1`
for each search clause matched. A document that matches one search clause
receives a score of `1`, while a document that matches three search clauses
receives a score of `3`. See the Examples section for scoring examples.

## Examples

The examples on this page use a collection named `users` containing the
following three documents:

## Note

The following example uses Javascript format. You can use the MongoDB Shell to
add these documents in this format. The Atlas UI requires JSON format.

    
    
    {  
      
      "_id" : ObjectId("5ed698faa1199b471010d70c"),  
      "name" : "Jim Hall",  
      "verified_user" : true,  
      "account" : {  
       "new_user" : true,  
       "active_user" : true  
      },  
      "teammates" : [  
       ObjectId("5ed6990aa1199b471010d70d"),  
       ObjectId("59b99dbdcfa9a34dcd7885c8")  
      ],  
      "region" : "East",  
      "account_created" : 2021-12-12T10:18:27.000+00:00,  
      "employee_number" : 257  
    }  
    {  
      "_id" : ObjectId("5ed6990aa1199b471010d70d"),  
      "name" : "Ellen Smith",  
      "verified_user" : true,  
      "account" : {  
       "new_user" : false,  
       "active_user" : true  
      },  
      "teammates" : [  
       ObjectId("5a9427648b0beebeb69537a5"),  
       ObjectId("59b99dbdcfa9a34dcd7881d1")  
      ],  
      "region" : "Southwest",  
      "account_created" : 2022-05-04T05:01:08.000+00:00,  
      "employee_number" : 258  
    }  
    {  
      "_id" : ObjectId("5ed6994fa1199b471010d70e"),  
      "name" : "Fred Osgood",  
      "verified_user" : false,  
      "account" : {  
       "new_user" : false,  
       "active_user" : false  
      },  
      "teammates" : [  
       ObjectId("5a9427648b0beebeb69589a1"),  
       ObjectId("59b99dbdcfa9a34dcd7897d3")  
      ],  
      "region" : "Northwest",  
      "account_created" : 2022-01-19T08:22:15.000+00:00  
      "employee_number" : 259  
    }  
  
The `users` collection is indexed with the following index definition:

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "account": {  
            "dynamic": true,  
            "type": "document"  
          },  
          "teammates": {  
            "type": "objectId"  
          },  
          "verified_user": {  
            "type": "boolean"  
          },  
          "region": {  
            "type": "string"  
          },  
          "account_created" : {  
            "type": "date"  
          },  
          "employee_number" : {  
            "type": "number"  
          }  
        }  
      }  
    }  
  
### Basic Examples

#### Boolean Examples

The following example uses the `equals` operator to search the `users`
collection for documents in which the `verified_user` field is set to `true`.

    
    
    db.users.aggregate([  
      
      {  
        "$search": {  
          "equals": {  
            "path": "verified_user",  
            "value": true  
          }  
        }  
      },  
      {  
        "$project": {  
          "name": 1,  
          "_id": 0,  
          "score": { "$meta": "searchScore" }  
        }  
      }  
    ])  
  
The above query returns the following results:

    
    
    { "name" : "Jim Hall", "score" : 1 }  
      
    { "name" : "Ellen Smith", "score" : 1 }  
  
The documents for "Jim Hall" and "Ellen Smith" each receive a score of `1`
because those documents have the `verified_user` field set to `true`.

The following example uses the `equals` operator to search the `users`
collection for documents in which the `account.new_user` field contains the
boolean value `true`.

    
    
    db.users.aggregate([  
      
      {  
        "$search": {  
          "equals": {  
            "path": "account.new_user",  
            "value": true  
          }  
        }  
      }  
    ])  
  
The above query returns the document for "Jim Hall", because that document
contains `"new_user": true` in the `account` object.

#### ObjectId Example

The following example uses the `equals` operator to search the `users`
collection for documents in which the `teammates` field contains the value
`ObjectId("5a9427648b0beebeb69589a1")`.

    
    
    db.users.aggregate([  
      
      {  
        "$search": {  
          "equals": {  
            "path": "teammates",  
            "value": ObjectId("5a9427648b0beebeb69589a1")  
          }  
        }  
      }  
    ])  
  
The above query returns the document for "Fred Osgood", because that document
contains `ObjectId("5a9427648b0beebeb69589a1")` in the `teammates` array.

#### Date Example

The following example uses the `equals` operator to search the `users`
collection for documents in which the `account_created` field contains the
value that matches `ISODate("2022-05-04T05:01:08.000+00:00")`.

    
    
    db.users.aggregate([  
      
      {  
        "$search": {  
          "equals": {  
            "path": "account_created",  
            "value": ISODate("2022-05-04T05:01:08.000+00:00")  
          }  
        }  
      }  
    ])  
  
The above query returns the document for "Ellen Smith", because that document
contains `"account_created": 2022-05-04T05:01:08.000+00:00`.

#### Number Example

The following example uses the `equals` operator to search the `users`
collection for documents in which the `employee_number` field contains the
value that matches `259`.

    
    
    db.users.aggregate([  
      
      {  
        "$search": {  
          "equals": {  
            "path": "employee_number",  
            "value": 259  
          }  
        }  
      }  
    ])  
  
The above query returns the document for "Fred Osgood", because that document
contains `"employee_number": 259`.

### Compound Examples

The following example uses the compound operator in conjunction with `must`,
`mustNot`, and `equals` to search for documents in which the `region` field is
`Southwest` and the `verified_user` field is not `false`.

    
    
    db.users.aggregate([  
      
      {  
        "$search": {  
          "compound": {  
            "must": {  
              "text": {  
                "path": "region",  
                "query": "Southwest"  
              }  
            },  
            "mustNot": {  
              "equals": {  
                "path": "verified_user",  
                "value": false  
              }  
            }  
          }  
        }  
      }  
    ])  
  
The above query returns the document for "Ellen Smith", which is the only one
in the collection which meets the search criteria.

The following example query has these search criteria:

  * The `verified_user` field must be set to `true`

  * One of the following must be true:

    * The `teammates` array contains the value `ObjectId("5ed6990aa1199b471010d70d")`

    * The `region` field is set to `Northwest`

    
    
    db.users.aggregate([  
      
      {  
        "$search": {  
          "compound": {  
            "must": {  
              "equals": {  
                "path": "verified_user",  
                "value": true  
              }  
            },  
            "should": [  
              {  
                "equals": {  
                  "path": "teammates",  
                  "value": ObjectId("5ed6990aa1199b471010d70d")  
                }  
              },  
              {  
                "text": {  
                  "path": "region",  
                  "query": "Northwest"  
                }  
              }  
            ],  
            "minimumShouldMatch": 1  
            }  
          }  
        },  
        {  
          "$project": {  
            "name": 1,  
            "_id": 0,  
            "score": { "$meta": "searchScore" }  
          }  
        }  
    ])  
  
The above query returns the following results:

    
    
    { "name" : "Jim Hall", "score" : 2 }  
      
  
The document for "Jim Hall" receives a score of `2` because it meets the
requirements for the `must` clause and the first of the two `should` clauses.

You can search for multiple ObjectIDs with a compound query. The following
example query uses the `compound` operator with a `should` clause to search
for three different ObjectIDs, at least two of which must appear to satisfy
the query.

    
    
    db.users.aggregate([  
      
      {  
        "$search": {  
          "compound": {  
            "should": [  
              {  
                "equals": {  
                  "path": "teammates",  
                  "value": ObjectId("5a9427648b0beebeb69537a5")  
                }  
              },  
              {  
                "equals": {  
                  "path": "teammates",  
                  "value": ObjectId("59b99dbdcfa9a34dcd7881d1")  
                }  
              },  
              {  
                "equals": {  
                  "path": "teammates",  
                  "value": ObjectId("5a9427648b0beebeb69579d0")  
                }  
              }  
            ],  
            "minimumShouldMatch": 2  
            }  
          }  
        },  
        {  
          "$project": {  
            "name": 1,  
            "_id": 0,  
            "score": { "$meta": "searchScore" }  
          }  
        }  
    ])  
  
The above query returns the following results:

    
    
    { "name" : "Ellen Smith", "score" : 2 }  
      
  
The document for "Ellen Smith" receives a score of `2` because it contains two
of the specified ObjectIDs in its `teammates` array.

← embeddedDocumentexists →

