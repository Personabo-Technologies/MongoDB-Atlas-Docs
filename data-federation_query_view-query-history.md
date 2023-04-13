Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Retrieve Federated Database Instance Query History

Share Feedback

On this page

  * Syntax
  * Fields
  * Output
  * Examples
  * Retrieve Details About the Queries
  * Filter `$queryHistory` Output for Specific Queries

You can retrieve details about the queries that were run in the past 7 days
using `$queryHistory` (aggregation). `$queryHistory` returns documents, one
per query, that contain information about the aggregate, find, and count
queries that were run in the past 7 days. You can filter on the fields
returned by `$queryHistory` in subsequent pipeline stages such as `$match`.

To run `$queryHistory`, use the db.aggregate helper. Run `$queryHistory`
against the `admin` database.

## Syntax

    
    
    {  
      
            $queryHistory: {  
              allUsers: <boolean>  
            }  
    }  
  
## Fields

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`allUsers`

|

boolean

|

Indicates whether or not to fetch documents for queries run by all users.
Valid values are:

  * `true` to fetch documents for queries run by all users

  * `false` to fetch documents for queries run by the current user only

You must have the `viewAllHistory` privilege on the cluster resource to use
this option. If you specify this option, but do not have `viewAllHistory`
privilege on the cluster resource, Data Federation returns an error.

If omitted, defaults to `false`.

|

Optional  
  
## Output

Each document returned by `$queryHistory` contains the following fields:

Field

|

Type

|

Description  
  
||  
  
`appName`

|

string

|

Name of the application that issued the query, if available.  
  
`background`

|

boolean

|

Flag that indicates whether the query ran in the background. Value can be one
of the following:

  * `true` \- if the query ran with the `background` option set to `true`

  * `false` \- if the query didn't specify the `background` option or if the query ran with the `background` option set to `false`

  
  
`collection`

|

string

|

Name of the collection on which the query was executed.  
  
`comment`

|

string

|

Comment associated with the query, if available. Empty if the query did not
include any comment.  
  
`db`

|

string

|

Name of the database that contains the collection on which the query was
executed.  
  
`endTime`

|

ISODate

|

Query completion time.  
  
`error`

|

string

|

Error, if any, returned by the query. Note that the query status `0` indicates
errors. Empty string if query ran successfully.  
  
`queryFilterComments`

|

array of any BSON type

|

Comment values included with the `$comment` operator inside the query
pipeline. Omitted if the query didn't include the `$comment` operator.

## Note

The $comment operator value can be any valid BSON type.  
  
`ok`

|

int

|

Status of the query. Value can be one of the following:

  * `1`, if query ran successfully

  * `0`, if there were errors when executing the query

  
  
`opid`

|

ObjectId

|

Unique identifier of the operation associated with the query in the ObjectId
format. The field value is the same as the `correlationID` that you can see in
errors and logs.  
  
`startTime`

|

ISODate

|

Query start time.  
  
`query`

|

document

|

Query operation that was run.  
  
`user`

|

string

|

Username of the user who ran the query, if available, in the following format:
`<authenticationDatabase>.<username>`. Note that the authentication database
for Atlas Data Federation is always `admin`. If the username of the user who
ran the query is not available, value is empty.  
  
## Examples

The examples below use the `Database0.Collection0` collection described in the
Get Started tutorial.

### Retrieve Details About the Queries

For the example below, suppose some of the queries described in the Getting
Started tutorial were run by `user1` on the `Collection0` collection in the
`Database0` database. The following example returns information on the queries
that were run by `user1` on the `Database0.Collection0` collection.

    
    
    db.aggregate([{$queryHistory: {}}]).pretty()  
      
  
`$queryHistory` returns one document for each query that ran on the
`Database0.Collection0` collection.

    
    
    {  
      
            "_id" : ObjectId("613fa06cf9521f85777d5be8"),  
            "query" : [  
                    {  
                            "$match" : {  
                                    "bedrooms" : 3,  
                                    "review_scores.review_scores_rating" : {  
                                            "$gt" : 79  
                                    }  
                            }  
                    },  
                    {  
                            "$count" : "numProperties"  
                    }  
            ],  
            "appName" : "MongoDB Shell",  
            "user" : "admin.user1",  
            "db" : "Database0",  
            "collection" : "Collection0",  
            "opid" : ObjectId("16a476f40ac6d97f22e4aa1f"),  
            "startTime" : ISODate("2021-09-13T19:02:35.589Z"),  
            "endTime" : ISODate("2021-09-13T19:03:08.730Z"),  
            "ok" : 1,  
            "background" : false  
    }  
    {  
            "_id" : ObjectId("613fa0d4f9521f85777d6bc0"),  
            "query" : [  
                    {  
                            "$match" : {  
                                    "bedrooms" : 3  
                            }  
                    },  
                    {  
                            "$sort" : {  
                                    "review_scores_rating" : -1  
                            }  
                    },  
                    {  
                            "$limit" : NumberLong(5)  
                    }  
            ],  
            "appName" : "MongoDB Shell",  
            "user" : "admin.user1",  
            "db" : "Database0",  
            "collection" : "Collection0",  
            "opid" : ObjectId("16a4770e387f300c22e4bdf2"),  
            "startTime" : ISODate("2021-09-13T19:04:28.184Z"),  
            "endTime" : ISODate("2021-09-13T19:04:52.898Z"),  
            "ok" : 1,  
            "background" : false  
    }  
    {  
            "_id" : ObjectId("613fa0eef9521f85777d6f6f"),  
            "query" : [  
                    {  
                            "$match" : {  
                                    "limit" : {  
                                            "$eq" : 10000  
                                    },  
                                    "products" : "Commodity"  
                            }  
                    },  
                    {  
                            "$limit" : NumberLong(5)  
                    }  
            ],  
            "appName" : "MongoDB Shell",  
            "user" : "admin.user1",  
            "db" : "Database0",  
            "collection" : "Collection0",  
            "opid" : ObjectId("16a477163555e4aa22e4c53b"),  
            "startTime" : ISODate("2021-09-13T19:05:02.342Z"),  
            "endTime" : ISODate("2021-09-13T19:05:18.774Z"),  
            "ok" : 1,  
            "background" : false  
    }  
    {  
            "_id" : ObjectId("613fa147f9521f85777d7b11"),  
            "query" : [  
                    {  
                            "$match" : {  
                                    "name" : /Lannister/  
                            }  
                    },  
                    {  
                            "$limit" : NumberLong(10)  
                    }  
            ],  
            "appName" : "MongoDB Shell",  
            "user" : "admin.user1",  
            "db" : "Database0",  
            "collection" : "Collection0",  
            "opid" : ObjectId("16a4771ba072c0a122e4c9bd"),  
            "startTime" : ISODate("2021-09-13T19:05:25.736Z"),  
            "endTime" : ISODate("2021-09-13T19:06:47.147Z"),  
            "ok" : 1,  
            "background" : false  
    }  
    {  
            "_id" : ObjectId("613fb9eccaba4e6430c7dcb7"),  
            "query" : [  
                    {  
                            "$group" : {  
                                    "_id" : "$movies",  
                                    "Collection0" : {  
                                            "$push" : "$title"  
                                    }  
                            }  
                    },  
                    {  
                            "$out" : {  
                                    "atlas" : {  
                                            "projectId" : "{PROJECT_ID}",  
                                            "clusterName" : "mySbx",  
                                            "db" : "my_test",  
                                            "coll" : "sample"  
                                    }  
                            }  
                    }  
            ],  
            "appName" : "MongoDB Shell",  
            "user" : "admin.user1",  
            "db" : "admin",  
            "collection" : "Collection0",  
            "opid" : ObjectId("16a47ceba943e9cc00c98c62"),  
            "startTime" : ISODate("2021-09-13T20:51:56.617Z"),  
            "endTime" : ISODate("2021-09-13T20:51:56.642Z"),  
            "ok" : 1,  
            "background" : true  
    }  
  
### Filter `$queryHistory` Output for Specific Queries

For the example below, suppose a query similar to the following is run against
the `Database0.Collection0` collection described in the Getting Started
tutorial. The query includes unique strings to help identify the query in the
results returned by the `$queryHistory` stage. You can attach a comment to a
query using the aggregate command `comment` option or the $comment operator.
This example uses both ways to attach the unique strings with the query.

    
    
    use Database0  
      
    db.Collection0.aggregate([ { $match: {"account_id": 557378, "$comment": "test"}},{$sort: {"transactions.symbol": -1}} ],{"comment":"exampleQuery"})  
  
comment Option Example

$comment Operator Example

To retrieve the query history using the string value of the `comment` option
of the aggregate command, run the following commands against the `admin`
database:

    
    
    use admin  
      
    db.aggregate([{$queryHistory: {}}, {$match: {"comment": "exampleQuery"}} ])  
  
`$queryHistory` finds the query that included the specified string and returns
results similar to the following:

    
    
    [  
      
      {  
        "_id": ObjectId("61e1e4c29e62172566d8e9b6"),  
        "query": [  
          { "$match": { "account_id": 557378, "$comment": "test" } },  
          { "$sort": { "transactions.symbol": -1 } }  
        ],  
        "comment": "exampleQuery",  
        "appName": "mongosh 1.1.8",  
        "user": "admin.user1",  
        "db": "Database0",  
        "collection": "Collection0",  
        "opid": ObjectId("16ca3ed2577016e68d60358c"),  
        "startTime": ISODate("2022-01-14T21:01:27.346Z"),  
        "endTime": ISODate("2022-01-14T21:01:54.627Z"),  
        "ok": 1,  
        "error": "",  
        "background": false,  
        "queryFilterComments": [ "test" ]  
      }  
    ]  
  
← Terminate a Running Federated Database Instance QueryDownload Query Logs →

