Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Determine Status of Queries Against Federated Database Instances

Share Feedback

On this page

  * Syntax
  * Output
  * Examples

You can determine the status of a running query using $currentOp
(aggregation). To run `$currentOp`, use the db.aggregate helper.

## Note

If you are an Admin user, you can view all queries using the `$currentOp`
`allUsers` option.

$currentOp must be run against the `admin` database.

## Note

If your aggregation pipeline only contains the $currentOp stage, Atlas Data
Federation doesn't enforce the limit on the maximum number of simultaneous
queries. You can run queries that only contain the $currentOp stage even after
you reach the maximum number of simultaneous queries.

## Syntax

    
    
    db.aggregate([{$currentOp: {} }])  
      
  
## Output

$currentOp returns documents with the following fields:

Field

|

Type

|

Description  
  
||  
  
`$currentOp.type`

|

string

|

Type of operation. Value is always `op`.  
  
`$currentOp.opid`

|

ObjectId

|

Unique identifier of the operation in ObjectId format. The field value is the
same as the `correlationID` that you can see in errors and logs.  
  
`$currentOp.client`

|

string

|

IP address (or hostname) and the ephemeral port of the client connection where
the operation originates.  
  
`$currentOp.clientMetadata`

|

Document

|

Additional client information such as the client:

  * Application name

  * Driver name and version

  * Operating system name, type, architecture, and version

  
  
`$currentOp.active`

|

boolean

|

Specifies whether the operation has started. Value is `true` if the operation
has started or completed and `false` if the operation is idle.  
  
`$currentOp.currentOpTime`

|

ISODate

|

Start time of the operation.  
  
`$currentOp.ns`

|

string

|

Namespace that the operation targets. A namespace consists of the database
name and the collection name concatenated with a dot (`.`); that is,
`"<database>.<collection>"`.  
  
`$currentOp.command`

|

Document

|

A document containing the command object associated with this operation.  
  
`$currentOp.msg`

|

string

|

A message that describes the status and progress of the operation.  
  
`$currentOp.progress`

|

Document

|

A document that contains the amount of work done for the operation.  
  
`$currentOp.progress.workDone`

|

integer

|

A number that increases as documents move through the pipeline, indicating
that progress has been made toward the completion of the query. This number is
not a percentage and cannot be used to estimate how much work remains.  
  
## Examples

For the example below, suppose one of the following queries is running on the
`airbnb` collection in the `sample` database described in the Get Started
tutorial.

find Command

aggregate Command

    
    
    db.airbnb.find( { "address.market" : "Porto", "review_scores.review_scores_rating": {$gt: 79}}).comment("Find properties in Porto")  
      
  
The following example returns information on the previous query running on the
`airbnb` collection in the `sample` database:

    
    
    db.aggregate([{$currentOp: {} }])  
      
  
$currentOp returns the following documents. The `workDone` field shows that
770 documents had been processed at the time that `$currentOp` was run.

    
    
    {  
      
            "type" : "op",  
            "opid" : ObjectId("1635fa35bf73f4320c6f99d0"),  
            "client" : "73.231.201.205:62351",  
            "clientMetadata" : {  
                   "application" : {  
                           "name" : "MongoDB Shell"  
                   },  
                   "driver" : {  
                           "name" : "MongoDB Internal Client",  
                           "version" : "4.2.0"  
                   },  
                   "os" : {  
                           "type" : "Darwin",  
                           "name" : "Mac OS X",  
                           "architecture" : "x86_64",  
                           "version" : "18.7.0"  
                    }  
            },  
            "active" : true,  
            "currentOpTime" : ISODate("2020-03-26T12:51:43.291Z"),  
            "ns" : "sample.airbnb",  
            "command" : {  
                    "find" : "airbnb",  
                    "filter" : {  
                          "address.market" : "Porto",  
                            "review_scores.review_scores_rating" : {  
                                    "$gt" : 79  
                            }  
                    },  
                  "comment" : "Find properties in Porto",  
                    "lsid" : {  
                            "id" : UUID("2211f8ac-56b2-4ba4-bb0c-2e5dd5b7cc21")  
                    },  
                    "$db" : "sample"  
            },  
            "msg" : "work done: 770",  
            "progress" : {  
              "workDone" : 770  
            }  
    }  
    {  
            "type" : "op",  
            "client" : "73.231.201.205:62353",  
            "clientMetadata" : {  
                    "application" : {  
                            "name" : "MongoDB Shell"  
                    },  
                    "driver" : {  
                            "name" : "MongoDB Internal Client",  
                      "version" : "4.2.0"  
                  },  
                    "os" : {  
                            "type" : "Darwin",  
                            "name" : "Mac OS X",  
                            "architecture" : "x86_64",  
                            "version" : "18.7.0"  
                    }  
            },  
            "active" : true,  
            "currentOpTime" : ISODate("2020-03-26T12:51:47.380Z"),  
            "ns" : "admin.$cmd.aggregate",  
            "command" : {  
                    "aggregate" : 1,  
                    "pipeline" : [  
                            {  
                                  "$currentOp" : {  
      
                                    }  
                            }  
                    ],  
                    "cursor" : {  
      
                    },  
                    "lsid" : {  
                            "id" : UUID("045ea383-65d7-4e88-a989-37b7a8da23bc")  
                    },  
                    "$db" : "admin"  
            },  
            "msg" : "work done: 0",  
            "progress" : {  
                    "workDone" : 0  
            }  
    }  
  
← Update a Federated Database Instance RegionTerminate a Running Federated
Database Instance Query →

