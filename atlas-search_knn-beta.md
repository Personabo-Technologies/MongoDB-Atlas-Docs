Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# knnBeta

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Behavior
  * Examples

## Note

This feature is in early access and available only for evaluation purposes, to
validate functionality, and to gather feedback from a small closed group of
early access users. It is not recommended for production deployments as we may
introduce breaking changes. This feature doesn't include formal consulting,
SLAs, or technical support obligations.

## Definition

`knnBeta`

    

The `knnBeta` operator uses Hierarchical Navigable Small Worlds algorithm to
perform semantic search. You can use Atlas Search support for kNN query to
search similar to a selected product, search for images, etc.

## Syntax

`knnBeta` has the following syntax:

    
    
    1| {  
    |  
    2|   $search: {  
    3|     "index": "<index name>", // optional, defaults to "default"  
    4|     "knnBeta": {  
    5|       "vector": [<array-of-numbers>],  
    6|       "path": "<field-to-search>",  
    7|       "filter": {<filter-specification>},  
    8|       "k": <number>,  
    9|       "score": {<options>}  
    10|     }  
    11|   }  
    12| }  
  
## Options

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`filter`

|

document

|

Any Atlas Search operator to filter the documents based on metadata or certain
search criteria, which can help narrow down the scope of vector search.

|

Optional  
  
`k`

|

number

|

Number of nearest neighbors to return. You can specify a number higher than
the number of documents to return (`$limit`) to increase accuracy.

|

Required  
  
`path`

|

string

|

Indexed knnVector type field to search. See Path Construction for more
information.

|

Required  
  
`vector`

|

array of numbers

|

Array of numbers of BSON types `int` or `double` that represent the query
vector. The array size must match the number of vector `dimensions` specified
in the index for the field.

|

Required  
  
## Behavior

You can run kNN queries against fields that were indexed as Atlas Search type
knnVector only.

You can use `$skip` and `$limit` after the `$search` stage to paginate the
`knnBeta` query results. However, the value that you specify for `k` must be
greater than or equal to the sum of the numbers you specify for `$skip` and
`$limit`.

## Example

The following query finds `150` nearest neighbors to the query, skips the
first `100` results, and limits the remaining number of results to `50`.

    
    
    1| db.<collection>.aggregate({  
    |  
    2|   "$search": {  
    3|     "knnBeta": {  
    4|       "vector": <array-of-numbers-to-search>,  
    5|       "path": <indexed-field-to-search>,  
    6|       "k": 150  
    7|     }  
    8|   }  
    9| },  
    10| {  
    11|   "$skip": 100  
    12| },  
    13| {  
    14|   "$limit": 50  
    15| })  
  
For the preceding query, the value of `k` (on line 6) shouldn't be less than
the sum of the number of documents skipped (on line 11), which is `100`, and
the number of documents returned (on line 14), which is `50`.

### Usage

You can use `knnBeta` within the compound operator to perform a hybrid of
keyword search and semantic search. `knnBeta` always returns only `k` results,
which is the number of nearest neighbors. Therefore, if you use `knnBeta`
inside the compound operator `must` clause with other operators, Atlas Search
uses the other operators for post-filtering of the semantic search results.
For pre-filtering, you can use the `filter` option inside `knnBeta`. On
sharded clusters, Atlas Search returns `k` results from each shard, but you
can use `$limit` to limit the total number of results.

Atlas Search scores the results for kNN queries in a fixed range from `0` to
`1` only. You can customize the default score for your keyword and semantic
subqueries using `boost` and other scoring options.

## Examples

The following queries search the sample `cheese_varieties` collection using
the `knnVector` operator. If you added the sample collection to a database on
your Atlas cluster and created the sample index definition for the collection,
you can switch to the database where you added this collection and run the
following queries against the collection.

Basic Example

Filter Example

Compound Example

The following query searches the `egVector` field using the `knnVector`
operator for `vector` dimensions and requests up to `3` nearest neighbors in
the results.

    
    
    1| db.cheese_varieties.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "index": "default",  
    5|       "knnBeta": {  
    6|         "vector": [-0.015739429742097855,0.04937680810689926,-0.1067470908164978,0.1293928325176239,-0.03162907809019089],  
    7|         "path": "egVector",  
    8|         "k": 3  
    9|       }  
    10|     }  
    11|   }  
    12| ])  
  
HIDE OUTPUT

    
    
    1| [  
    |  
    2|   {  
    3|     _id: 3,  
    4|     name: 'feta',  
    5|     description: "Greek brined white cheese made from sheep's milk or from a mixture of sheep and goat's milk.",  
    6|     countryOfOrigin: 'Greece',  
    7|     egVector: [  
    8|       -0.015739429742097855,  
    9|       0.04937680810689926,  
    10|       -0.1067470908164978,  
    11|       0.1293928325176239,  
    12|       -0.03162907809019089  
    13|     ],  
    14|     aging: 'about 3 months',  
    15|     yearProduced: 2021,  
    16|     brined: true  
    17|   },  
    18|   {  
    19|     _id: 1,  
    20|     name: 'mozzarella',  
    21|     description: "Italian cheese typically made from buffalo's milk.",  
    22|     countryOfOrigin: 'Italy',  
    23|     egVector: [  
    24|       -0.09950768947601318,  
    25|       -0.02402166835963726,  
    26|       -0.046839360147714615,  
    27|       0.06274440884590149,  
    28|       -0.0920015424489975  
    29|     ],  
    30|     aging: 'none',  
    31|     yearProduced: 2022,  
    32|     brined: false  
    33|   },  
    34|   {  
    35|     _id: 2,  
    36|     name: 'parmesan',  
    37|     description: "Italian hard, granular cheese produced from cow's milk.",  
    38|     countryOfOrigin: 'Italy',  
    39|     egVector: [  
    40|       -0.04228218272328377,  
    41|       -0.024080513045191765,  
    42|       -0.029374264180660248,  
    43|       -0.04369240626692772,  
    44|       -0.01295427419245243  
    45|     ],  
    46|     aging: 'at least 1 year',  
    47|     yearProduced: 2021,  
    48|     brined: false  
    49|   }  
    50| ]

