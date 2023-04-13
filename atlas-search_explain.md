Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Retrieve Query Plan and Execution Statistics

Share Feedback

On this page

  * Syntax
  * Verbosity
  * Explain Response
  * Limitations
  * Examples
  * `queryPlanner`
  * `executionStats`

## Important

You can run Atlas Search queries with `explain` in `mongosh`. However, this
feature is not available for MongoDB Compass.

The Atlas Search query returns information about the `$search` query plan and
execution statistics when the query is run with the `explain` method. When you
run a query with `explain`, Atlas Search returns a BSON document containing
information about how the query was run.

## Tip

### See also:

explain command

## Syntax

    
    
    db.<myCollection>.explain("<verbosity>").aggregate([  
      
      {  
        $search: {  
          "<operator>": {  
            "<operator-options>"  
          }  
        }  
      }  
    ])  
  
## Verbosity

Verbosity mode controls the behavior of `explain` and the amount of
information returned. Value can be one of the following:

|  
  
|  
  
queryPlanner (default)

|

Information about the query plan. Does not include the `stats` field, which
contains execution statistics for the query.  
  
executionStats

|

Information about the query plan including the `stats` field, which contains
execution statistics for the query.  
  
allPlansExecution

|

Information about the query plan including the `stats` field, which contains
execution statistics for the query.  
  
## Tip

### See also:

Verbosity Modes

## Explain Response

The `explain` response is a BSON document with keys and values describing the
execution statistics for the query. The `explain` document in the result set
contains the following fields:

Option

|

Type

|

Necessity

|

Purpose  
  
|||  
  
`path`

|

string

|

Optional

|

Path to the operator, only if it isn't the root.  
  
`type`

|

string

|

Required

|

Name of the Lucene Query that the Atlas Search operator created. See Lucene
Query Structured Summary for more information.  
  
`analyzer`

|

string

|

Optional

|

Atlas Search analyzer used with the query.  
  
`args`

|

document

|

Required

|

Lucene query information. See Lucene Query Structured Summary for more
information.  
  
`stats`

|

document

|

Optional

|

Explain Timing Breakdown for the query if `explain` ran with `executionStats`
or `allPlansExecution` verbosity.  
  
## Limitations

You can't run facet queries with `explain`.

## Examples

The following examples use the `movies` collection in the `sample_mflix`
database.

## Tip

If you've already loaded the sample dataset, follow the Get Started with Atlas
Search tutorial to create an index definition and run Atlas Search queries.

### `queryPlanner`

The following example uses the text operator to query the `title` field with
the `queryPlanner` verbosity mode.

    
    
    db.movies.explain("queryPlanner").aggregate([  
      
      {  
        $search: {  
          "text": {  
            "path": "title",  
            "query": "yark",  
            "fuzzy": {  
              "maxEdits": 1,  
              "maxExpansions": 100,  
            }  
          }  
        }  
      }  
    ])  
  
The query returns the following results. To learn more about the `explain`
response elements, see Explain Response.

    
    
    {  
      
      "stages" : [  
        {  
          "$_internalSearchMongotRemote" : {  
            "mongotQuery" : {  
              "text" : {  
                "path" : "title",  
                "query" : "yark",  
                "fuzzy" : {  
                  "maxEdits" : 1,  
                  "maxExpansions" : 100  
                }  
              }  
            },  
            "explain" : {  
              "type" : "BooleanQuery",  
              "args" : {  
                "must" : [ ],  
                "mustNot" : [ ],  
                "should" : [  
                  {  
                    "type" : "BoostQuery",  
                    "args" : {  
                      "query" : {  
                        "type" : "TermQuery",  
                        "args" : {  
                          "path" : "title",  
                          "value" : "ark"  
                        }  
                      },  
                      "boost" : 0.6666666269302368  
                    }  
                  },  
                  {  
                    "type" : "BoostQuery",  
                    "args" : {  
                      "query" : {  
                        "type" : "TermQuery",  
                        "args" : {  
                          "path" : "title",  
                          "value" : "yard"  
                        }  
                      },  
                      "boost" : 0.75  
                    }  
                  },  
                  {  
                    "type" : "BoostQuery",  
                    "args" : {  
                      "query" : {  
                        "type" : "TermQuery",  
                        "args" : {  
                          "path" : "title",  
                          "value" : "mark"  
                        }  
                      },  
                      "boost" : 0.75  
                    }  
                  },  
                  {  
                    "type" : "BoostQuery",  
                    "args" : {  
                      "query" : {  
                        "type" : "TermQuery",  
                        "args" : {  
                          "path" : "title",  
                          "value" : "park"  
                        }  
                      },  
                      "boost" : 0.75  
                    }  
                  },  
                  {  
                    "type" : "BoostQuery",  
                    "args" : {  
                      "query" : {  
                        "type" : "TermQuery",  
                        "args" : {  
                          "path" : "title",  
                          "value" : "dark"  
                        }  
                      },  
                      "boost" : 0.75  
                    }  
                  },  
                  {  
                    "type" : "BoostQuery",  
                    "args" : {  
                      "query" : {  
                        "type" : "TermQuery",  
                        "args" : {  
                          "path" : "title",  
                          "value" : "york"  
                        }  
                      },  
                      "boost" : 0.75  
                    }  
                  }  
                ],  
                "filter" : [ ],  
                "minimumShouldMatch" : 0  
              }  
            }  
          }  
        },  
        {  
          "$_internalSearchIdLookup" : { }  
        }  
      ],  
      "serverInfo" : {  
        "host" : "atlas-example-shard-00-01.mongodb.net",  
        "port" : 27017,  
        "version" : "4.4.3",  
        "gitVersion" : "913d6b62acfbb344dde1b116f4161360acd8fd13"  
      },  
      "ok" : 1,  
      "$clusterTime" : {  
        "clusterTime" : Timestamp(1612457287, 1),  
        "signature" : {  
          "hash" : BinData(0,"kzn7hY7NOduVIqcfx+40ENKbMKQ="),  
          "keyId" : NumberLong("1234567890123456789")  
        }  
      },  
      "operationTime" : Timestamp(1612457287, 1)  
    }  
  
### `executionStats`

The following example uses the autocomplete operator to query the `title`
field with the `executionStats` verbosity mode.

    
    
    db.movies.explain("executionStats").aggregate([  
      
      {  
        "$search": {  
          "autocomplete": {  
            "path": "title",  
            "query": "pre",  
            "fuzzy": {  
              "maxEdits": 1,  
              "prefixLength": 1,  
              "maxExpansions": 256  
            }  
          }  
        }  
      }  
    ])  
  
The query returns the following results. To learn more about the `explain`
response elements, see Explain Response.

    
    
    {  
      
      "stages" : [  
        {  
          "$_internalSearchMongotRemote" : {  
            "mongotQuery" : {  
              "autocomplete" : {  
                "path" : "title",  
                "query" : "pre",  
                "fuzzy" : {  
                  "maxEdits" : 1,  
                  "prefixLength" : 1,  
                  "maxExpansions" : 256  
                }  
              }  
            },  
            "explain" : {  
              "type" : "MultiTermQueryConstantScoreWrapper",  
              "args" : {  
                "queries" : [  
                  {  
                    "type" : "DefaultQuery",  
                    "args" : {  
                      "queryType" : "AutomatonQuery"  
                    },  
                    "stats" : {  
                      "context" : {  
                        "nanosElapsed" : NumberLong(0)  
                      },  
                      "match" : {  
                        "nanosElapsed" : NumberLong(0)  
                      },  
                      "score" : {  
                        "nanosElapsed" : NumberLong(0)  
                      }  
                    }  
                  }  
                ]  
              },  
              "stats" : {  
                "context" : {  
                  "nanosElapsed" : NumberLong(816418),  
                  "invocationCounts" : {  
                    "createWeight" : NumberLong(1),  
                    "createScorer" : NumberLong(2)  
                  }  
                },  
                "match" : {  
                  "nanosElapsed" : NumberLong(3849778),  
                  "invocationCounts" : {  
                    "nextDoc" : NumberLong(656)  
                  }  
                },  
                "score" : {  
                  "nanosElapsed" : NumberLong(35349),  
                  "invocationCounts" : {  
                    "score" : NumberLong(655)  
                  }  
                }  
              }  
            }  
          },  
          "nReturned" : NumberLong(0),  
          "executionTimeMillisEstimate" : NumberLong(20)  
        },  
        {  
          "$_internalSearchIdLookup" : { },  
          "nReturned" : NumberLong(0),  
          "executionTimeMillisEstimate" : NumberLong(20)  
        }  
      ],  
      "serverInfo" : {  
        "host" : "atlas-example-shard-00-01.mongodb.net",  
        "port" : 27017,  
        "version" : "4.4.3",  
        "gitVersion" : "913d6b62acfbb344dde1b116f4161360acd8fd13"  
      },  
      "ok" : 1,  
      "$clusterTime" : {  
        "clusterTime" : Timestamp(1612454116, 1),  
        "signature" : {  
          "hash" : BinData(0,"OY+SMPmdK//g6rFZkvSCQr3c3hM="),  
          "keyId" : NumberLong("1234567890123456789")  
        }  
      },  
      "operationTime" : Timestamp(1612454116, 1)  
    }

