Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Customize and Normalize the Score in Results

Share Feedback

On this page

  * Modify the Score
  * `boost`
  * Fields
  * Examples
  * `constant`
  * Examples
  * `embedded`
  * Fields
  * Examples
  * `function`
  * Expressions
  * Examples
  * Normalize the Score
  * Examples

Every document returned by an Atlas Search query is assigned a score based on
relevance, and the documents included in a result set are returned in order
from highest score to lowest.

## Modify the Score

Many factors can influence a document's score, including:

  * The position of the search term in the document,

  * The frequency of occurrence of the search term in the document,

  * The type of operator the query uses,

  * The type of analyzer the query uses.

The score assigned to a returned document is part of the document's metadata.
You can include each returned document's score along with the result set by
using a `$project` in your aggregation pipeline. After a `$project` stage, you
do not need to include a descending `$sort` because Atlas Search returns the
documents from highest score to lowest by default.

The following example query uses a `$project` stage to add a field named
`score` to the returned documents:

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "text": {  
    5|         "query": "Helsinki",  
    6|         "path": "plot"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     $project: {  
    12|       plot: 1,  
    13|       title: 1,  
    14|       score: { $meta: "searchScore" }  
    15|     }  
    16|   }  
    17| ])  
  
More information about the Lucene scoring algorithm can be found in the Lucene
documentation.

The following score modifying options are available to all operators. For
details and examples, click any of the following options:

  * `boost`

  * `constant`

  * `embedded`

  * `function`

### `boost`

The `boost` option multiplies a result's base score by a given number or the
value of a numeric field in the documents. For example, you can use `boost` to
increase the importance of certain matching documents in the result.

## Note

  * The `boost` and `constant` options can't be used together.

  * The `boost` option with `path` is the same as multiplying using the `function` option with a path expression.

#### Fields

The `boost` option takes the following fields:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`value`

|

float

|

Conditional

|

Number to multiply the default base score by. Value must be a positive number.
Either `value` or `path` is required, but you can't specify both.  
  
`path`

|

string

|

Conditional

|

Name of the numeric field whose value to multiply the default base score by.
Either `path` or `value` is required, but you can't specify both.  
  
`undefined`

|

float

|

Optional

|

Numeric value to substitute for `path` if the numeric field specified through
`path` is not found in the documents. If omitted, defaults to `0`. You can
specify this only if you specify `path`.  
  
#### Examples

The following examples use the `movies` collection in the `sample_mflix`
database. If you have the sample dataset on your cluster, you can create the
Atlas Search `default` index and run the example queries on your cluster.

The sample compound queries demonstrate how to increase the importance of one
search criteria over another. The queries include a `$project` stage to
exclude all fields except `title` and `score`.

`value` Field Example

`path` Field Example

In the following example, the compound operator uses text operator to search
for the term `Helsinki` in the `plot` and `title` fields. The query for the
`title` field uses `score` with the `boost` option to multiply the score
results by 3, as specified in the `value` field.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "compound": {  
    5|         "should": [{  
    6|           "text": {  
    7|             "query": "Helsinki",  
    8|             "path": "plot"  
    9|           }  
    10|         },  
    11|         {  
    12|           "text": {  
    13|             "query": "Helsinki",  
    14|             "path": "title",  
    15|             "score": { "boost": { "value": 3 } }  
    16|           }  
    17|         }]  
    18|       }  
    19|     }  
    20|   },  
    21|   {  
    22|     "$limit": 5  
    23|   },  
    24|   {  
    25|     $project: {  
    26|       "_id": 0,  
    27|       "title": 1,  
    28|       "score": { "$meta": "searchScore" }  
    29|     }  
    30|   }  
    31| ])  
  
The above query returns the following results, in which the score for
documents where the `title` matches the query term is multiplied by 3 from its
base value:

    
    
    [  
      
      {  
        plot: 'Epic tale about two generations of men in a wealthy Finnish family, spanning from the 1960s all the way through the early 1990s. The father has achieved his position as director of the ...',  
        title: 'Kites Over Helsinki',  
        score: 12.2470121383667  
      },  
      {  
        plot: 'Alex is Finlander married to an Italian who works as a taxi driver in Berlin. One night in his taxi come two men with a briefcase full of money. Unluckily for Alex, they are being chased by...',  
        title: 'Helsinki-Naples All Night Long',  
        score: 9.56808090209961  
      },  
      {  
        plot: 'The recession hits a couple in Helsinki.',  
        title: 'Drifting Clouds',  
        score: 4.5660295486450195  
      },  
      {  
        plot: 'Two teenagers from Helsinki are sent on a mission by their drug dealer.',  
        title: 'Sairaan kaunis maailma',  
        score: 4.041563034057617  
      },  
      {  
        plot: 'A murderer tries to leave his criminal past in East Helsinki and make a new life for his family',  
        title: 'Bad Luck Love',  
        score: 3.6251673698425293  
      }  
    ]  
  
### `constant`

The `constant` option replaces the base score with a specified number.

## Note

The `constant` and `boost` options may not be used together.

#### Examples

The following example uses the default index on the `sample_mflix.movies`
collection to query the `plot` and `title` fields using the compound operator.
In the query, the text operator uses `score` with the `constant` option to
replace all score results with `5` for results that match the query against
the `title` field only.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "compound": {  
    5|         "should": [{  
    6|           "text": {  
    7|             "query": "tower",  
    8|             "path": "plot"  
    9|           }  
    10|         },  
    11|         {  
    12|           "text": {  
    13|             "query": "tower",  
    14|             "path": "title",  
    15|             "score": { "constant": { "value": 5 } }  
    16|           }  
    17|         }]  
    18|       }  
    19|     }  
    20|   },  
    21|   {  
    22|     $project: {  
    23|       "_id": 0,  
    24|       "title": 1,  
    25|       "score": { "$meta": "searchScore" }  
    26|     }  
    27|   }  
    28| ])  
  
The above query returns the following results, in which the score for
documents that match the query against the `title` field only is replaced with
the specified `constant` value:

    
    
    1| [  
    |  
    2|   {  
    3|     plot: 'Several months after witnessing a murder, residents of Tower Block 31 find themselves being picked off by a sniper, pitting those lucky enough to be alive into a battle for survival.',  
    4|     title: 'Tower Block',  
    5|     score: 8.15460205078125  
    6|   },  
    7|   {  
    8|     plot: "When a group of hard-working guys find out they've fallen victim to their wealthy employer's Ponzi scheme, they conspire to rob his high-rise residence.",  
    9|     title: 'Tower Heist',  
    10|     score: 5  
    11|   },  
    12|   {  
    13|     plot: 'Toru Kojima and his friend Koji are young student boys with one thing in common - they both love to date older women. Koji is a playboy with several women, young and older, whereas Toru is a romantic with his heart set on on certain lady.',  
    14|     title: 'Tokyo Tower',  
    15|     score: 5  
    16|   },  
    17|   {  
    18|     plot: 'A middle-aged mental patient suffering from a split personality travels to Italy where his two personalities set off all kinds of confusing developments.',  
    19|     title: 'The Leaning Tower',  
    20|     score: 5  
    21|   },  
    22|   {  
    23|     plot: 'A documentary that questions the cost -- and value -- of higher education in the United States.',  
    24|     title: 'Ivory Tower',  
    25|     score: 5  
    26|   }  
    27| ]  
  
### `embedded`

## Note

This option can be used with embeddedDocument operator only.

The `embedded` option allows you to configure how to:

  * Aggregate scores of multiple matching embedded documents

  * Modify the score of an embeddedDocument operator after aggregating scores from matching embedded documents

## Note

The Atlas Search embeddedDocuments index option, embeddedDocument operator,
and `embedded` scoring option are in preview. When an Atlas Search index on a
replica set or single MongoDB shard reaches Lucene's two billion document
limit, Atlas Search doesn't index new documents or apply updates to existing
documents for that index. A solution to accommodate this limitation will be in
place when this feature is generally available. To troubleshoot any issues
related to using this feature, contact Support.

#### Fields

The `embedded` option takes the following fields:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`aggregate`

|

string

|

Optional

|

Configures how to combine scores of matching embedded documents. Value must be
one of the following aggregation strategies:

  * `sum` \- (Default) Sum the score of all matching embedded documents.

  * `maximum` \- Choose the greatest score of all matching embedded documents.

  * `minimum` \- Choose the least high score of all matching embedded documents.

  * `mean` \- Choose the average (arithmetic mean) score of all matching embedded documents. Atlas Search include scores of matching embedded documents only when computing the average. Atlas Search doesn't count embedded documents that don't satisfy query predicates as documents with scores of zero.

If omitted, defaults to `sum`.  
  
`outerScore`

|

Scoring Option

|

Optional

|

Specifies the score modification to apply after applying the aggregation
strategy.  
  
#### Examples

The following sample query uses an index named `default` on the
`sample_analytics.transactions` collection. The index configures an
`embeddedDocuments` field on documents in the `transactions` array, `string`
fields for `transactions.symbol` and `transactions.transaction_code` fields,
and a `number` field on the `transaction_count` field.

The sample query on the `transactions` field, which contains an array of
documents, includes a `$limit` stage to limit the output to `10` results and a
`$project` stage to:

  * Exclude all fields except `account_id` and `transaction_count`.

  * Add a field named `score` that applies an aggregation strategy and further score modification after.

## Note

You can use `function` inside the `score` option of the embeddedDocument
operator's `operator`. However, for function score expressions that require
the `path` option, the numeric field that you specify as the `path` for the
expression must be inside the embeddedDocument operator's `path`. For example,
in the example query below, the field `transactions.amount` that is specified
inside the `score` option of the `compound` operator on line 24 is inside in
the `embeddedDocument` operator's path `transactions` on line 4.

The query searches for accounts that have bought `AMD` and multiplies the
largest single `AMD` purchase (by number of shares) by the `log1p` value of
the number of transactions that the account has made in this period. It ranks
the accounts based on the following:

  * Number of `AMD` bought in a single transaction

  * Number of transactions in the last period

    
    
    1| db.transactions.aggregate({  
    |  
    2|   "$search": {  
    3|     "embeddedDocument": {  
    4|       "path": "transactions",  
    5|       "operator": {  
    6|         "compound": {  
    7|           "must": [  
    8|             {  
    9|               "text": {  
    10|                 "path": "transactions.symbol",  
    11|                 "query": "amd"  
    12|               }  
    13|             },  
    14|             {  
    15|               "text": {  
    16|                 "path": "transactions.transaction_code",  
    17|                 "query": "buy"  
    18|               }  
    19|             }  
    20|           ],  
    21|           "score": {  
    22|             "function": {  
    23|               "path": {  
    24|                 "value": "transactions.amount",  
    25|                 "undefined": 1.0  
    26|               }  
    27|             }  
    28|           }  
    29|         }  
    30|       },  
    31|       "score": {  
    32|         "embedded": {  
    33|           "aggregate": "maximum",  
    34|           "outerScore": {  
    35|             "function": {  
    36|               "multiply": [  
    37|                 {  
    38|                   "log1p": {  
    39|                     "path": {  
    40|                       "value": "transaction_count"  
    41|                     }  
    42|                   }  
    43|                 },  
    44|                 {  
    45|                   "score": "relevance"  
    46|                 }  
    47|               ]  
    48|             }  
    49|           }  
    50|         }  
    51|       }  
    52|     }  
    53|   }  
    54| },  
    55| { "$limit": 10 },  
    56| {  
    57|   "$project": {  
    58|     "_id": 0,  
    59|     "account_id": 1,  
    60|     "transaction_count": 1,  
    61|     "score": { $meta: "searchScore" }  
    62|   }  
    63| })  
  
Atlas Search ranks accounts that have made many transactions in the last
period and bought many `AMD` in a single transaction highly.

    
    
    1| [  
    |  
    2|   { account_id: 467651, transaction_count: 99, score: 19982 },  
    3|   { account_id: 271554, transaction_count: 96, score: 19851.822265625 },  
    4|   { account_id: 71148, transaction_count: 99, score: 19840 },  
    5|   { account_id: 408143, transaction_count: 100, score: 19836.76953125 },  
    6|   { account_id: 977774, transaction_count: 98, score: 19822.64453125 },  
    7|   { account_id: 187107, transaction_count: 96, score: 19754.470703125 },  
    8|   { account_id: 492843, transaction_count: 97, score: 19744.998046875 },  
    9|   { account_id: 373169, transaction_count: 93, score: 19553.697265625 },  
    10|   { account_id: 249078, transaction_count: 89, score: 19436.896484375 },  
    11|   { account_id: 77690, transaction_count: 90, score: 19418.017578125 }  
    12| ]  
  
### `function`

The `function` option allows you to alter the final score of the document
using a numeric field . You can specify the numeric field for computing the
final score through an expression. If the final result of the function score
is less than `0`, Atlas Search replaces the score with `0`.

## Note

You can use `function` inside the `score` option of the embeddedDocument
operator's `operator`. However, for function score expressions that require
the `path` option, the numeric field that you specify as the `path` for the
expression must be inside the embeddedDocument operator's `path`.

#### Expressions

Use the following expressions with the `function` option to alter the final
score of the document:

  * Arithmetic expressions, which add or multiply a series of numbers.

  * Constant expressions, which allow a constant number in the function score.

  * Gaussian decay expressions, which decay, or reduces, the scores by multiplying at a specified rate.

  * Path expressions, which incorporate an indexed numeric field value into a function score.

  * Score expressions, which return the relevance score assigned by Atlas Search.

  * Unary expressions, which are expressions that take a single argument. In Atlas Search, you can calculate the log10(x) or log10(x+1) of a specified number.

Arithmetic

Constant

Gaussian

Path

Score

Unary

An arithmetic expression adds or multiplies a series of numbers. For example,
you can use arithmetic expression to modify relevance ranking through a
numeric field from a data enrichment pipeline. It must include one of the
following options:

Option

|

Type

|

Description  
  
||  
  
`add`

|

array of expressions

|

Adds a series of numbers. Takes an array of expressions, which can have
negative values. Array length must be greater than or equal to `2`.

## Example

Arithmetic Expression Syntax

    
    
    | "function": {  
      
      "add": [  
        {"path": "rating"},  
        {"score": "relevance"}  
      ]  
    }  
  
Atlas Search uses the `path` and `score` expressions to add the following:

  * Numeric value of the `rating` field or `0`, if the `rating` field is not present in the document

  * Relevance score, which is the score Atlas Search assigns based on relevance

  
  
`multiply`

|

array of expressions

|

Multiplies a series of numbers. Takes an array of expressions, which can have
negative values. Array length must be greater than or equal to `2`.

## Example

Arithmetic Expression Syntax

    
    
    | "function": {  
      
      "multiply": [  
        {  
          "path": {  
            "value": "popularity",  
            "undefined": 2.5  
          }  
        },  
        {"score": "relevance"},  
        {"constant": 0.75}  
      ]  
    }  
  
Atlas Search uses the `path`, `score`, and `constant` expressions to alter the
final score of the document. It multiplies the following:

  * Numeric value of the path expression, which is the numeric value of the `popularity` field or `2.5`, if the `popularity` field is not present in the document

  * Relevance score, which is the score Atlas Search assigns based on relevance

  * Constant value of `0.75`

  
  
## Note

You can't replace an arithmetic expression that evaluates to `undefined` with
a constant value.

#### Examples

The following examples use the default index on the `sample_mflix.movies`
collection to query the `title` field. The sample queries include a `$limit`
stage to limit the output to `5` results and a `$project` stage to exclude all
fields except `title` and `score`.

Arithmetic

Constant

Gaussian

Path

Score

Unary

## Example

In this example, the text operator uses `score` with the `function` option to
multiply the following:

  * Numeric value of the path expression, which is the value of the `imdb.rating` field in the documents or `2`, if the `imdb.rating` field is not in the document

  * Relevance score, or the current score of the document

    
    
    db.movies.aggregate([{  
      
      "$search": {  
        "text": {  
          "path": "title",  
          "query": "men",  
          "score": {  
            "function":{  
              "multiply":[  
                {  
                  "path": {  
                    "value": "imdb.rating",  
                    "undefined": 2  
                  }  
                },  
                {  
                  "score": "relevance"  
                }  
              ]  
            }  
          }  
        }  
      }  
    },  
    {  
      $limit: 5  
    },  
    {  
      $project: {  
        "_id": 0,  
        "title": 1,  
        "score": { "$meta": "searchScore" }  
      }  
    }])  
  
The preceding query returns the following results, in which the score is
replaced with the specified `function` value:

    
    
    { "title" : "Men...", "score" : 23.431293487548828 }  
      
    { "title" : "12 Angry Men", "score" : 22.080968856811523 }  
    { "title" : "X-Men", "score" : 21.34803581237793 }  
    { "title" : "X-Men", "score" : 21.34803581237793 }  
    { "title" : "Matchstick Men", "score" : 21.05954933166504 }  
  
## Normalize the Score

You can normalize your `$search` query score in the range from `0` to `1` in
the subsequent stages of your aggregation pipeline. You can use the following
stages after your `$search` stage in the following order to normalize the
score:

  * `$addFields`
    
        {  
      
      "$addFields": {  
        "score": {  
          "$meta": "searchScore"  
        }  
      }  
    }  
  
  * `$setWindowFields`
    
        {  
      
      "$setWindowFields": {  
        "output": {  
          "maxScore": {  
            "$max": "$score"  
          }  
        }  
      }  
    }  
  
  * `$addFields`
    
        {  
      
      "$addFields": {  
        "normalizedScore": {  
          "$divide": [  
            "$score", "$maxScore"  
          ]  
        }  
      }  
    }  
  

### Examples

The following examples demonstrate how to normalize the score for some of the
queries against the `sample_mflix.movies` collection in the preceding Examples
using the `$addFields` and `$setWindowFields` stages after the `$search`
stage.

Basic

Arithmetic

Gaussian

Path

Unary

    
    
    1| db.movies.aggregate([{  
    |  
    2|   "$search": {  
    3|     "text": {  
    4|       "query": "Helsinki",  
    5|       "path": "plot"  
    6|     }  
    7|   }  
    8| },  
    9| {  
    10|   "$limit": 5  
    11| },  
    12| {  
    13|   "$project": {  
    14|     "_id": 0,  
    15|     "title": 1,  
    16|     "score": 1,  
    17|     "maxScore": 1,  
    18|     "normalizedScore": 1  
    19| },  
    20| {  
    21|   "$addFields": {  
    22|     "score": {  
    23|       "$meta": "searchScore"  
    24|     }  
    25|   }  
    26| },  
    27| {  
    28|   "$setWindowFields": {  
    29|     "output": {  
    30|       "maxScore": {  
    31|         "$max": "$score"  
    32|       }  
    33|     }  
    34|   }  
    35| },  
    36| {  
    37|   "$addFields": {  
    38|     "normalizedScore": {  
    39|       "$divide": [  
    40|         "$score", "$maxScore"  
    41|       ]  
    42|     }  
    43|   }  
    44| }])  
  
HIDE OUTPUT

    
    
    1| [  
    |  
    2|   {  
    3|     _id: ObjectId("573a139af29313caabcf0042"),  
    4|     plot: 'The recession hits a couple in Helsinki.',  
    5|     title: 'Drifting Clouds',  
    6|     score: 4.5660295486450195,  
    7|     maxScore: 4.5660295486450195,  
    8|     normalizedScore: 1  
    9|   },  
    10|   {  
    11|     _id: ObjectId("573a139af29313caabcf0353"),  
    12|     plot: 'Two teenagers from Helsinki are sent on a mission by their drug dealer.',  
    13|     title: 'Sairaan kaunis maailma',  
    14|     score: 4.041563034057617,  
    15|     maxScore: 4.5660295486450195,  
    16|     normalizedScore: 0.8851372929150143  
    17|   },  
    18|   {  
    19|     _id: ObjectId("573a13a0f29313caabd039cd"),  
    20|     plot: 'A murderer tries to leave his criminal past in East Helsinki and make a new life for his family',  
    21|     title: 'Bad Luck Love',  
    22|     score: 3.6251673698425293,  
    23|     maxScore: 4.5660295486450195,  
    24|     normalizedScore: 0.79394303764817  
    25|   },  
    26|   {  
    27|     _id: ObjectId("573a13a3f29313caabd0efac"),  
    28|     plot: 'A murderer tries to leave his criminal past in East Helsinki and make a new life for his family',  
    29|     title: 'Bad Luck Love',  
    30|     score: 3.6251673698425293,  
    31|     maxScore: 4.5660295486450195,  
    32|     normalizedScore: 0.79394303764817  
    33|   },  
    34|   {  
    35|     _id: ObjectId("573a13c0f29313caabd63214"),  
    36|     plot: 'Two teen girls from a very restrictive Conservative Laestadian faith community, go alone to Helsinki for the first time.',  
    37|     title: 'Forbidden Fruit',  
    38|     score: 3.6251673698425293,  
    39|     maxScore: 4.5660295486450195,  
    40|     normalizedScore: 0.79394303764817  
    41|   }  
    42| ]  
  
Atlas Search results contain the following scores:

  * The modified score for the `$search` query in the `score` field from the `$addFields` stage.

  * The maximum score assigned to the documents in the results in the `maxScore` field from the `$setWindowFields` stage.

  * The normalized score in the `normalizedScore` field from the `$addFields` stage, which is computed by dividing the modified score in `$score` by the maximum score in `$maxScore` using $divide.

← Construct a Query PathHighlight Search Terms in Results →

