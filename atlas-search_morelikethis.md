Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# moreLikeThis

Share Feedback

On this page

  * Definition
  * Behavior
  * Usage
  * Syntax
  * Options
  * Limitations
  * Examples

## Definition

`moreLikeThis`

    

The `moreLikeThis` operator returns documents similar to input documents. The
`moreLikeThis` operator allows you to build features for your applications
that display similar or alternative results based on one or more given
documents.

## Behavior

When you run a `moreLikeThis` query, Atlas Search performs these actions:

  * Extracts a limited number of most representative terms based on the input documents that you specify in the operator's `like` option.

  * Creates a disjunction ( _OR_ ) query to find similar documents based on the most representative terms and returns the results.

The `moreLikeThis` operator performs a search for similar documents using the
analyzer that you specify in the index configuration. If you omit the analyzer
in the index definition, the `moreLikeThis` operator uses the default standard
analyzer. If you specify multiple analyzers, the `moreLikeThis` operator runs
the input text through each analyzer, searches, and returns results for all
analyzers.

To view the disjunction ( _OR_ ) that Atlas Search constructs to find similar
documents, use explain with your `moreLikeThis` operator query.

## Usage

Before you can run the `moreLikeThis` operator query, we recommend that you
retrieve one or more input documents. To retrieve input documents, you can do
one of the following:

  * Run a query, such as find(), or another MQL query to find BSON documents.

  * Run any aggregation pipeline that returns BSON documents.

  * Use any other source of documents in your application.

Once you identify the input documents, you can pass them to the `moreLikeThis`
operator.

When you run a `moreLikeThis` operator query, Atlas Search returns the
original input document in the query results. To omit the input document from
the query results, use the `moreLikeThis` operator in a compound operator
query and exclude the input document by its `_id` using the `equals` operator
in the mustNot clause.

## Syntax

`moreLikeThis` has the following syntax:

    
    
     {  
      
       "$search": {  
         "index": index name, // optional, defaults to "default"  
         "moreLikeThis": {  
           "like": [  
             {  
               <"field-name">: <"field-value">,  
               ...  
             },  
             ...  
           ],  
           ...  
         }  
       }  
     }  
  
## Options

`moreLikeThis` uses the following option to constuct a query:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`like`

|

one BSON document or an array of documents

|

One or more BSON documents that Atlas Search uses to extract representative
terms to query for.

|

yes  
  
## Limitations

You can't use the `moreLikeThis` operator to query non-string values. To
search for non-string values, you can combine a `moreLikeThis` query with a
near, range, or any other operator in a compound operator query.

You can't use the `moreLikeThis` operator inside the embeddedDocument operator
to query documents in an array.

## Examples

The examples use the `movies` collection in the `sample_mflix` database. Each
example in this section uses a different index definition to demonstrate
different features of the operator.

Before you run the example queries on your cluster, load the sample data on
your Atlas cluster, and create the suggested index. To learn more about
creating an Atlas Search index using the UI, API, or CLI, see Create an Atlas
Search Index. The index definitions use the name `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

### Example 1: Single Document with Multiple Fields

The following example uses the `moreLikeThis` operator to find documents that
are similar to multiple field values. For this example, the index defition
contains dynamic mappings to dynamically index all dynamically indexable field
types in the collection. Your index definition for the `sample_mflix.movies`
collection should look similar to the following.

    
    
    {  
      
      "mappings": {  
        "dynamic": true  
      }  
    }  
  
## Example

The following query searches for movies that are similar to the input movie
title "The Godfather" and input movie genre "action". It includes a `$limit`
stage to limit the output to `5` results and a `$project` stage to exclude all
fields except `title`, `released`, and `genres`.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|     moreLikeThis: {  
    5|      like:  
    6|       {  
    7|         "title": "The Godfather",  
    8|         "genres": "action"  
    9|       }  
    10|     }  
    11|    }  
    12|   },  
    13|   { "$limit": 5},  
    14|   {  
    15|     $project: {  
    16|       "_id": 0,  
    17|       "title": 1,  
    18|       "released": 1,  
    19|       "genres": 1  
    20|     }  
    21|   }  
    22| ])  
  
HIDE OUTPUT

    
    
    [  
      
     { genres: [ 'Comedy', 'Drama', 'Romance' ], title: 'Godfather' },  
     {  
      genres: [ 'Crime', 'Drama' ],  
      title: 'The Godfather',  
      released: ISODate("1972-03-24T00:00:00.000Z")  
     },  
     {  
      genres: [ 'Crime', 'Drama' ],  
      title: 'The Godfather: Part II',  
      released: ISODate("1974-12-20T00:00:00.000Z")  
     },  
     {  
      genres: [ 'Crime', 'Drama' ],  
      title: 'The Godfather: Part III',  
      released: ISODate("1990-12-26T00:00:00.000Z")  
     },  
     {  
      genres: [ 'Action' ],  
      title: 'The Defender',  
      released: ISODate("1994-07-28T00:00:00.000Z")  
     }  
    ]  
  
Atlas Search results contain movies similar to the input movie title "The
Godfather" and input movie genre "action".

### Example 2: Input Document Excluded in Results

The following example uses `find()` to identify an input document, and then
uses the `moreLikeThis` operator to find similar documents. For this example,
the index definition uses static mappings to index only the `title`, `genres`,
and `_id` fields.

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "dynamic": false,  
    4|     "fields": {  
    5|       "title": {  
    6|         "type": "string"  
    7|       },  
    8|       "genres": {  
    9|         "type": "string"  
    10|       },  
    11|       "_id": {  
    12|         "type": "objectId"  
    13|       }  
    14|     }  
    15|   }  
    16| }  
  
## Example

The following `find()` query finds the movie with the title "The Godfather"
and stores the result inside `movie`. It specifies that the results should
only contain the `title` and `genres` fields for the matching documents. Note
that, by default, the `find ()` command always returns the `_id` field, the
value for which might be different on your cluster.

    
    
    movie = db.movies.find( { title: "The Godfather" }, { genres: 1, title: 1} ).toArray()  
      
  
HIDE OUTPUT

    
    
    [  
      
     {  
      _id: ObjectId("573a1396f29313caabce4a9a"),  
      genres: [ 'Crime', 'Drama' ],  
      title: 'The Godfather'  
     }  
    ]  
  
The following query uses a compound operator with the `moreLikeThis` operator
to query the `title` and `genres` fields and the equals operator to exclude
the input document using the following clauses:

  * The `must` clause to query for movies similar to the movie stored in `movie`.

  * The `mustNot` clause to exclude the input document from results by its `_id` value. Note that the `_id` value used in the query matches the `_id` value in the results of the preceding `find()` query.

The query limits the output to `5` results. The query uses a `$project` stage
to include the `_id`, `title`, `released`, and `genres` fields in the results.

## Note

Before you run this query, replace the value of the `_id` field on line 13
with the value of the `_id` field in your query results.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|        "compound":{  
    5|           "must":[{  
    6|             "moreLikeThis": {  
    7|               "like": movie  
    8|             }  
    9|           }],  
    10|           "mustNot":[{  
    11|             "equals": {  
    12|                "path": "_id",  
    13|                "value": ObjectId ("573a1396f29313caabce4a9a")  
    14|             }  
    15|           }]  
    16|          }  
    17|        }  
    18|      },  
    19| {"$limit": 5},  
    20| {  
    21|  "$project": {  
    22|    "_id": 1,  
    23|    "title": 1,  
    24|    "released": 1,  
    25|    "genres": 1  
    26|   }  
    27|  }  
    28| ])  
  
HIDE OUTPUT

    
    
    [  
      
     {  
      _id: ObjectId("573a13acf29313caabd27afc"),  
      genres: [ 'Comedy', 'Drama', 'Romance' ],  
      title: 'Godfather'  
     },  
     {  
      _id: ObjectId("573a1396f29313caabce557f"),  
      genres: [ 'Crime', 'Drama' ],  
      title: 'The Godfather: Part II',  
      released: ISODate("1974-12-20T00:00:00.000Z")  
     },  
     {  
      _id: ObjectId("573a1398f29313caabcebf7b"),  
      genres: [ 'Crime', 'Drama' ],  
      title: 'The Godfather: Part III',  
      released: ISODate("1990-12-26T00:00:00.000Z")  
     },  
     {  
      _id: ObjectId("573a1399f29313caabceed8d"),  
      genres: [ 'Action' ],  
      title: 'The Defender',  
      released: ISODate("1994-07-28T00:00:00.000Z")  
     },  
     {  
      _id: ObjectId("573a139af29313caabcef2a0"),  
      genres: [ 'Action' ],  
      title: 'The Enforcer',  
      released: ISODate("1995-03-02T00:00:00.000Z")  
     }  
    ]  
  
Atlas Search results include documents that are similar to the query term `The
Godfather` in the `action` genre. However, the results don't include the
document that was excluded by its `_id`, which is
`ObjectId("573a1396f29313caabce4a9a")`.

### Example 3: Multiple Analyzers

The following example uses `find()` to identify input documents, and then uses
a `moreLikeThis` operator to find similar documents. For this example, the
index definition uses static mappings to index the fields in the
`sample_mflix.movies` collection with different analyzers. The index
definition:

  * Configures an index on the `_id`, `title` and `genres` fields.

  * Analyzes the `title` field using the `lucene.standard` analyzer and an alternate analyzer named `keywordAnalyzer` that uses the `lucene.keyword` analyzer.

  * Analyzes and searches the fields using the `lucene.english` analyzer.

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "dynamic": false,  
    4|     "fields": {  
    5|       "title": {  
    6|         "type": "string",  
    7|         "analyzer": "lucene.standard",  
    8|         "multi": {  
    9|           "keywordAnalyzer": {  
    10|             "type": "string",  
    11|             "analyzer": "lucene.keyword"  
    12|           }  
    13|         }  
    14|       },  
    15|       "genres": {  
    16|         "type": "string"  
    17|       },  
    18|       "_id": {  
    19|         "type": "objectId"  
    20|       }  
    21|     }  
    22|   },  
    23|   "analyzer": "lucene.english"  
    24| }  
  
## Example

The following `find()` query retrieves the movies with the title "Alice in
Wonderland" and stores the results in `movie`. It specifies that the results
should only contain the `title` and `genres` fields for the matching
documents. Note that, by default, the `find()` command always returns the
`_id` field, the value for which might be different on your cluster.

    
    
    movie = db.movies.find( { title: "Alice in Wonderland" }, { genres: 1, title: 1} ).toArray  
      
  
HIDE OUTPUT

    
    
    [  
      
      {  
       _id: ObjectId("573a1394f29313caabcde9ef"),  
       plot: 'Alice stumbles into the world of Wonderland. Will she get home? Not if the Queen of Hearts has her way.',  
       title: 'Alice in Wonderland'  
      },  
      {  
       _id: ObjectId("573a1398f29313caabce963d"),  
       plot: 'Alice is in Looking Glass land, where she meets many Looking Glass creatures and attempts to avoid the Jabberwocky, a monster that appears due to her being afraid.',  
       title: 'Alice in Wonderland'  
      },  
      {  
       _id: ObjectId("573a1398f29313caabce9644"),  
       plot: 'Alice is in Looking Glass land, where she meets many Looking Glass creatures and attempts to avoid the Jabberwocky, a monster that appears due to her being afraid.',  
       title: 'Alice in Wonderland'  
      },  
      {  
       _id: ObjectId("573a139df29313caabcfb504"),  
       plot: `The wizards behind The Odyssey (1997) and Merlin (1998) combine Lewis Carroll's "Alice in Wonderland" and "Through the Looking Glass" into a two-hour special that just gets curiouser and curiouser.`,  
       title: 'Alice in Wonderland'  
      },  
      {  
       _id: ObjectId("573a13bdf29313caabd5933b"),  
       plot: "Nineteen-year-old Alice returns to the magical world from her childhood adventure, where she reunites with her old friends and learns of her true destiny: to end the Red Queen's reign of terror.",  
       title: 'Alice in Wonderland'  
      }  
    ]  
  
The following example uses a compound operator to query the `title` and
`genres` fields using the following clauses:

  * The `should` clause uses the `moreLikeThis` operator to search for documents similar to the document in `movie`. Note that the `title` field is analyzed with both the `lucene.standard` and `lucene.keyword` analyzers.

  * The `mustNot` clause specifies that one of the input documents, specified by its `_id` value, must not be included in the results.

The query limits the results list to `10` documents. The query uses a
`$project` stage to include the `_id`, `title`, and `genres` fields in the
results.

## Example

    
    
    1| db.movies.aggregate([  
    |  
    2| {  
    3|    $search: {  
    4|      "compound": {  
    5|        "should": [{  
    6|           "moreLikeThis": {  
    7|              "like": movie  
    8|           }  
    9|        }],  
    10|      "mustNot": [  
    11|      {  
    12|      "equals": {  
    13|      "path": "_id",  
    14|       "value": ObjectId ("573a1394f29313caabcde9ef")  
    15|     }  
    16|    }]  
    17|  }  
    18|   }  
    19|   },  
    20|  { $limit: 10 },  
    21|           {  
    22|  $project: {  
    23|      "title": 1,  
    24|      "genres": 1,  
    25|      "_id": 1  
    26|    }  
    27|   }  
    28|  ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
       _id: ObjectId("573a1398f29313caabce963d"),  
       genres: [ 'Adventure', 'Family', 'Fantasy' ],  
       title: 'Alice in Wonderland'  
      },  
      {  
       _id: ObjectId("573a1398f29313caabce9644"),  
       genres: [ 'Adventure', 'Family', 'Fantasy' ],  
       title: 'Alice in Wonderland'  
      },  
      {  
       _id: ObjectId("573a139df29313caabcfb504"),  
       genres: [ 'Adventure', 'Comedy', 'Family' ],  
       title: 'Alice in Wonderland'  
      },  
      {  
       _id: ObjectId("573a13bdf29313caabd5933b"),  
       genres: [ 'Adventure', 'Family', 'Fantasy' ],  
       title: 'Alice in Wonderland'  
      },  
      {  
       _id: ObjectId("573a1396f29313caabce3e7e"),  
       genres: [ 'Comedy', 'Drama' ],  
       title: 'Alex in Wonderland'  
      },  
      {  
       _id: ObjectId("573a13bdf29313caabd5a44b"),  
       genres: [ 'Drama' ],  
       title: 'Phoebe in Wonderland'  
      },  
      {  
       _id: ObjectId("573a139af29313caabcf0e23"),  
       genres: [ 'Documentary' ],  
       title: 'Wonderland'  
      },  
      {  
       _id: ObjectId("573a139ef29313caabcfcebc"),  
       genres: [ 'Drama' ],  
       title: 'Wonderland'  
      },  
      {  
       _id: ObjectId("573a13a0f29313caabd03dab"),  
       genres: [ 'Drama' ],  
       title: 'Wonderland'  
      },  
      {  
       _id: ObjectId("573a13abf29313caabd2372a"),  
       genres: [ 'Crime', 'Drama', 'Mystery' ],  
       title: 'Wonderland'  
      }  
    ]  
  
The following query uses explain with the preceding query to show the
disjunction ( _OR_ ) that Atlas Search constructs to find similar documents.

    
    
    db.movies.explain("queryPlanner").aggregate([  
      
     {  
       $search: {  
         "compound": {  
           "should": [{  
              "moreLikeThis": {  
                 "like": [{  
                    "title": "Alice in Wonderland"  
                 }]  
              }  
           }],  
         "mustNot": [  
         {  
         "equals": {  
         "path": "_id",  
          "value": ObjectId ("573a1394f29313caabcde9ef")  
        }  
       }]  
     }  
      }  
      },  
    { $limit: 10 },  
              {  
    $project: {  
         "title": 1,  
         "genres": 1,  
         "_id": 1  
       }  
     }  
    ])  
  
HIDE OUTPUT

    
    
    {  
      
     explainVersion: '1',  
       stages: [  
         {  
          '$_internalSearchMongotRemote': {  
             mongotQuery: {  
             compound: {  
             should: [  
              {  
                moreLikeThis: { like: [ { title: 'Alice in Wonderland' } ] }  
              }  
             ],  
             mustNot: [  
              {  
                equals: {  
                  path: '_id',  
                  value: ObjectId("573a1394f29313caabcde9ef")  
                }  
              }  
             ]  
          }  
         },  
         explain: {  
          type: 'BooleanQuery',  
            args: {  
             must: [],  
             mustNot: [  
               {  
                 path: 'compound.mustNot',  
                 type: 'ConstantScoreQuery',  
                 args: {  
                   query: {  
                   type: 'TermQuery',  
                 args: {  
                    path: '_id',  
                    value: '[57 3a 13 94 f2 93 13 ca ab cd e9 ef]'  
                   }  
                  }  
                }  
               }  
             ],  
             should: [  
              {  
                path: 'compound.should',  
                type: 'BooleanQuery',  
                args: {  
                 must: [],  
                 mustNot: [],  
                 should: [  
                  {  
                   type: 'TermQuery',  
                   args: { path: 'title', value: 'in' }  
                  },  
                  {  
                    type: 'TermQuery',  
                    args: {  
                      path: 'title.keywordAnalyzer',  
                      value: 'Alice in Wonderland'  
                    }  
                   },  
                  {  
                    type: 'TermQuery',  
                    args: { path: 'title', value: 'wonderland' }  
                  },  
                  {  
                    type: 'TermQuery',  
                    args: { path: 'title', value: 'alice' }  
                  }  
                 ],  
                 filter: [],  
                  minimumShouldMatch: 0  
                 }  
                }  
              ],  
                filter: [],  
                 minimumShouldMatch: 0  
                }  
               }  
              }  
             },  
     { '$_internalSearchIdLookup': {} },  
     { '$limit': Long("10") },  
     { '$project': { _id: true, title: true, genres: true } }  
      ],  
     serverInfo: {  
     ...  
     },  
     serverParameters: {  
     ...  
     },  
     command: {  
       aggregate: 'movies',  
         pipeline: [  
           {  
            '$search': {  
               compound: {  
                 should: [  
                   {  
                     moreLikeThis: { like: [ { title: 'Alice in Wonderland' } ] }  
                   }  
                 ],  
                 mustNot: [  
                  {  
                    equals: {  
                      path: '_id',  
                      value: ObjectId("573a1394f29313caabcde9ef")  
                    }  
                  }  
                 ]  
               }  
              }  
            },  
      { '$limit': 10 },  
      { '$project': { title: 1, genres: 1, _id: 1 } }  
      ],  
      cursor: {},  
      '$db': 'sample_mflix'  
      },  
      ok: 1,  
      '$clusterTime': {  
      clusterTime: Timestamp({ t: 1659133479, i: 1 }),  
      signature: {  
         hash: Binary(Buffer.from("865d9ef1187ae1a74c4a0da1e29882aebcf2be7c", "hex"), 0),  
         keyId: Long("7123262728533180420")  
      }  
     },  
     operationTime: Timestamp({ t: 1659133479, i: 1 })  
     }  
  
← geoWithinnear →

