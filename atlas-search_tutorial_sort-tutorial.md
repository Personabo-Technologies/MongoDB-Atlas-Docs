Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Sort Your Atlas Search Results for Your Perfomance Needs

Select your language

MongoDB Shell

On this page

  * Create the Atlas Search Index
  * Procedure
  * Sort Your Search Results
  * Sort Numbers for Speed
  * Sort Dates for Speed
  * Sort Strings for Precision
  * Sort Strings for Speed and Precision

## Important

The procedures in this tutorial might not be sufficient to optimize search
query performance for all use cases. To provide feedback on your use case, use
the MongoDB Feedback Engine.

This tutorial describes the various ways to sort your Atlas Search results
based on your performance needs. You can sort for speed, precision, or for
both.

First, this tutorial creates an index with static mappings for the `title`,
`year` and `released` fields in the `sample_mflix.movies` collection on
`mongot`. It also uses the storedSource option for the `title` field only.
Storing fields on `mongot` allows you to perform interim operations such as
sort on documents with a minimum number of fields and avoid full document
lookup in the interim stages. Then, the tutorial shows how to sort the query
results using the field stored on `mongot`.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Create the Atlas Search Index

In this section, you will create an Atlas Search index on the `released`,
`title`, and `year` fields in the `sample_mflix.movies` collection and
configure the `storesdSource` option for the `title` field to store that field
on `mongot`.

### Procedure

1

#### Navigate to the Atlas Search page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

#### Click Create Index.

3

#### Select a Configuration Method and click Next.

  * For a guided experience, select Visual Editor.

  * To edit the raw index definition, select JSON Editor.

4

#### Enter the Index Name, and set the Database and Collection.

  1. In the Index Name field, enter `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

  2. In the Database and Collection section, find the `sample_mflix` database, and select the `movies` collection.

5

#### Specify an index definition.

Use the Visual Editor or the JSON Editor in the Atlas user interface to create
an index definition that:

  * Indexes the `released` and `year` fields as date and number field types respectively.

  * Indexes the `title` field as `string` and `autocomplete` types.

  * Analyzes the title field using the `lucene.keyword` analyzer for the `string` type.

  * Stores the `title` field on `mongot`.

Visual Editor

JSON Editor

  1. Click Next.

  2. Click Refine Your Index.

  3. In the Index Configuration section, toggle to disable Dynamic Mapping.

  4. In the Field Mappings section, click Add Field and add the following fields by clicking Add after configuring the settings for each field.

Field Name

|

Data Type Configuration  
  
|  
  
`title`

|

    1. Click Data Type dropdown and select String.

    2. Change the Index Analyzer to `lucene.keyword`.

    3. Click Add Another Data Type and select Autocomplete from the dropdown.

    4. Change the Max Grams and Min Grams to `5`, select `false` for Fold Diacritics, and keep Tokenization as `edgeGram`.  
  
`year`

|

    1. Click Data Type dropdown and select Number.

    2. Keep the default value for all **Number Properties**.  
  
`released`

|

    1. Click Data Type dropdown.

    2. Select Date from the dropdown.  
  
  5. In the Stored Source Fields section, click Specified and do the following:

    1. Select `title` from the dropdown under Fields to Include in Stored Source.

    2. Click Add.

  6. Click Save Changes.

6

#### Click Create Search Index.

7

#### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

8

#### Wait for the index to finish building.

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

## Sort Your Search Results

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
example in this section.

* * *

You can sort your search results in multiple ways. The queries in this section
demonstrate how to sort your search results using the following:

  * near and wildcard operators for querying the data

  * returnStoredSource option for retrieving the field stored on `mongot`

  * score options for altering the scores of matching results

### Sort Numbers for Speed

MongoDB Shell

Compass

Go

Java (Sync)

Node.js

Python

1

#### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

#### Use the `sample_mflix` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_mflix  
      
  
MongoDB Shell

3

#### Run an Atlas Search query against the indexed field and sort the results
very fast.

The following query shows how to sort a numeric field to decrease the time
your query executes. It uses the near operator to search for movies that were
released in and about five years before or after 2015.

## Note

When you use `pivot` on a numeric field, its unit of measure is equal to the
data type of the `path` field. Since the query is on the `year` field, and the
unit of measure is in years, then `pivot` is also in years. To learn more, see
near.

The query uses the following pipeline stages:

  * `$search` stage to search the `year` field.

  * `$limit` stage to limit the output to `5` results.

  * `$project` stage to exclude all fields except `_id`, `title`, `released`, and `year`.

## Note

This method omits the `$sort` stage because the near operator automatically
sorts the results in ascending order based on `_id` field.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "near": {  
    5|         "path": "year",  
    6|         "origin": 2015,  
    7|         "pivot": 5  
    8|       }  
    9|     }  
    10|   },  
    11|   {  
    12|     $limit: 5  
    13|   },  
    14|   {  
    15|     $project: {  
    16|       title: 1,  
    17|       released: 1,  
    18|       year: 1  
    19|     }  
    20|   }  
    21| ])  
  
MongoDB Shell

HIDE OUTPUT

    
    
    {  
      
      _id: ObjectId("573a13adf29313caabd2b765"),  
      title: 'Jurassic World',  
      released: ISODate("2015-06-12T00:00:00.000Z"),  
      year: 2015  
    },  
    {  
      _id: ObjectId("573a13b1f29313caabd3719d"),  
      title: 'The Stanford Prison Experiment',  
      released: ISODate("2015-07-17T00:00:00.000Z"),  
      year: 2015  
    },  
    {  
      _id: ObjectId("573a13b5f29313caabd42f7f"),  
      year: 2015,  
      title: 'Ex Machina',  
      released: ISODate("2015-04-24T00:00:00.000Z")  
    },  
    {  
      _id: ObjectId("573a13b5f29313caabd44e2b"),  
      year: 2015,  
      title: 'Ant-Man',  
      released: ISODate("2015-07-17T00:00:00.000Z")  
    },  
    {  
      _id: ObjectId("573a13b8f29313caabd4d540"),  
      title: 'The Danish Girl',  
      released: ISODate("2015-11-27T00:00:00.000Z"),  
      year: 2015  
    }  
  
### Sort Dates for Speed

MongoDB Shell

Compass

Go

Java (Sync)

Node.js

Python

1

#### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

#### Use the `sample_mflix` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_mflix  
      
  
MongoDB Shell

3

#### Run an Atlas Search query against the indexed field and sort the results
very fast.

The following query shows how to sort a date field to decrease the time your
query executes. It uses the following operators:

  * wildcard operator to search for movie titles that begin with `Summer`.

  * near operator to search for movies that were released in and about five months before or after April 18, 2014.

## Note

When you use `pivot` on a date field, its unit of measure is in milliseconds.
Atlas Search calculates a score for each document based on how close the date
field is to the specified date and then sorts them in descending order based
on their score. To learn more, see near.

The query uses the following pipeline stages:

  * `$search` stage to search the `title` and `released` fields.

  * `$limit` stage to limit the output to `5` results.

  * `$project` stage to:

    * Exclude all fields except `title`, and `released`.

    * Add a field named `score`.

## Note

This method omits the `$sort` stage because the near operator automatically
sorts the results in descending order based on `score` field.

    
    
    1| db.movies.aggregate([  
    |  
    2| {  
    3|   $search: {  
    4|     "compound": {  
    5|       "filter": [{  
    6|         "wildcard": {  
    7|           "query": "Summer*",  
    8|           "path": "title"  
    9|         }  
    10|       }],  
    11|       "must": [{  
    12|         "near": {  
    13|           "pivot": 13149000000,  
    14|           "score": {  
    15|             "boost": {  
    16|               "value": 100  
    17|             }  
    18|           },  
    19|         "path": "released",  
    20|         "origin": ISODate("2014-04-18T00:00:00.000+00:00")  
    21|         }  
    22|       }]  
    23|     }  
    24|   }  
    25| },  
    26| {  
    27|   $project: {  
    28|     "_id": 0,  
    29|     "title": 1,  
    30|     "released": 1,  
    31|     "score": {  
    32|       "$meta": "searchScore"  
    33|     }  
    34|   }  
    35| },  
    36| {  
    37|   $limit: 5  
    38| }])  
  
MongoDB Shell

HIDE OUTPUT

    
    
    {  
      
      title: 'Summer of Blood',  
      released: ISODate("2014-04-17T00:00:00.000Z"),  
      score: 99.34720611572266  
    },  
    {  
      title: 'Summer in February',  
      released: ISODate("2014-01-17T00:00:00.000Z"),  
      score: 62.58031463623047  
    },  
    {  
      title: 'Summertime',  
      released: ISODate("2014-08-01T00:00:00.000Z"),  
      score: 59.17375564575195  
    },  
    {  
      title: 'Summer Nights',  
      released: ISODate("2015-01-28T00:00:00.000Z"),  
      score: 34.810577392578125  
    },  
    {  
      title: 'Summer Games',  
      released: ISODate("2012-02-08T00:00:00.000Z"),  
      score: 15.98293399810791  
    }  
  
### Sort Strings for Precision

## Note

This method is highly resource intensive and not recommended in production.

MongoDB Shell

Compass

Go

Java (Sync)

Node.js

Python

1

#### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

#### Use the `sample_mflix` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_mflix  
      
  
MongoDB Shell

3

#### Run an Atlas Search query against the indexed field and sort for
precision.

The following query shows how to sort a string field to increase the precision
of your query. It searches for titles that begin with `Prince` or `Prance` and
sorts the results by the `constant` score assigned to the different titles.

The query uses the following pipeline stages:

  * `$search` to search the `title` field using the `should` clause with the wildcard operator to search for titles that begin with `Prance` and `Prince`. Each subquery specifies a score that replaces the base score for matching results with the specified number, which allows the results to be sorted based on the score. The scores from highest to lowest sort the movie titles alphabetically.

  * `$limit` stage to limit the output to `5` results.

  * `$project` stage to:

    * Exclude all fields except `title`.

    * Add a field named `score`.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       compound: {  
    5|         "should": [{  
    6|           "wildcard": {  
    7|             "query": ["Prance*"],  
    8|             "path": "title",  
    9|             "score": {  
    10|               "constant": {  
    11|                 "value": 99  
    12|               }  
    13|             },  
    14|             "allowAnalyzedField": true  
    15|           }  
    16|         },  
    17|         {  
    18|           "wildcard": {  
    19|             "query": ["Prince*"],  
    20|             "path": "title",  
    21|             "score": {  
    22|               "constant": {  
    23|                 "value": 95  
    24|               }  
    25|             }  
    26|           }  
    27|         }]  
    28|       },  
    29|     }  
    30|   },  
    31|   {  
    32|     $limit: 5  
    33|   },  
    34|   {  
    35|     $project: {  
    36|       "_id": 0,  
    37|       "title": 1,  
    38|       "score": { "$meta": "searchScore" }  
    39|     }  
    40|   }  
    41| ])  
  
MongoDB Shell

HIDE OUTPUT

    
    
    {  
      
      title: 'Prancer',  
      score: 99  
    },  
    {  
      title: 'Prancer Returns',  
      score: 99  
    },  
    {  
      title: 'Prince of Foxes',  
      score: 95  
    },  
    {  
      title: 'Prince of the City',  
      score: 95  
    },  
    {  
      title: 'Prince of Darkness',  
      score: 95  
    }  
  
The Atlas Search results contain documents with movie titles that begin with
`Prance` and `Prince`. Atlas Search returns titles with `Prance` followed by
`Prince` because Atlas Search returns documents from highest to lowest score
and you replaced the scores of these terms with a constant value of `99` and
`95` respectively. If you want to sort the results by `Prince` first, modify
its score value to be greater than `Prance`.

### Sort Strings for Speed and Precision

MongoDB Shell

Compass

Go

Java (Sync)

Node.js

Python

1

#### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

#### Use the `sample_mflix` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_mflix  
      
  
MongoDB Shell

3

#### Run an Atlas Search query against the indexed field and sort speed and
precision.

The following query shows how to sort a string field to increase the overall
performance of your query. It searches for titles that begin with the term
`Happy` using the autocomplete operator and retrieves the stored fields to
sort your results.

The query uses the following pipeline stages:

  * `$search` stage to search the `title` field and retrieve the field stored on `mongot`.

  * `$limit` stage to limit the output to `5` results.

  * `$sort` stage to sort the titles in descending order.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "autocomplete": {  
    5|         "path": "title",  
    6|         "query": "Happy"  
    7|       },  
    8|       "returnStoredSource": true  
    9|     }  
    10|   },  
    11|   {  
    12|     $limit: 5  
    13|   },  
    14|   {  
    15|     $sort: {  
    16|       title: -1  
    17|     }  
    18|   }  
    19| ])  
  
MongoDB Shell

HIDE OUTPUT

    
    
    {  
      
      _id: ObjectId("573a13bef29313caabd5aeba"),  
      title: 'Happy-Go-Lucky'  
    },  
    {  
      _id: ObjectId("573a1396f29313caabce4efc"),  
      title: 'Happy New Year'  
    },  
    {  
      _id: ObjectId("573a13ddf29313caabdb4efe"),  
      title: 'Happy New Year'  
    },  
    { _id: ObjectId("573a13c5f29313caabd70f55"), title: 'Happy Feet 2' },  
    {  
      _id: ObjectId("573a13c3f29313caabd6b1b2"),  
      title: 'Happy Ever Afters'  
    }  
  
← How to Define a Custom Analyzer and Run an Atlas Search Diacritic-
Insensitive QueryHow to Run Atlas Search String Queries Against Date and
Numeric Fields →

