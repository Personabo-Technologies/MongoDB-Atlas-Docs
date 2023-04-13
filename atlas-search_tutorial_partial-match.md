Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run Partial Match Atlas Search Queries

Select your language

MongoDB Shell

On this page

  * Create the Atlas Search Index
  * Run a Case-Sensitive Partial Match Query

This tutorial describes how to create an index on the `sample_mflix.movies`
collection and run partial string queries against the `plot` field. To return
matches for partial string queries, you can use one of the following
operators:

  * The autocomplete operator, which allows you to search the specified fields for a word or phrase that contains the sequence of characters that you specify with your query.

  * The phrase operator, which allows you to search the specified fields for documents that contain the terms in your query string at the distance you specify between the terms.

  * The regex operator, which allows you to search the specified fields for strings using regular expression.

  * The wildcard operator, which allows you to search the specified fields using special characters in your query to match any character.

This tutorial takes you through the following steps:

  1. Set up an Atlas Search index on the `plot` field in the `sample_mflix.movies` collection.

  2. Run Atlas Search query for a partial string against the `plot` field in the `sample_mflix.movies` collection using autocomplete, phrase, regex, and wildcard operators.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Create the Atlas Search Index

In this section, you will create an Atlas Search index on the `plot` field in
the `sample_mflix.movies` collection for running partial match queries against
those fields.

1

### Navigate to the Atlas Search page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

### Click Create Index.

3

### Select a Configuration Method and click Next.

  * For a guided experience, select Visual Editor.

  * To edit the raw index definition, select JSON Editor.

4

### Enter the Index Name, and set the Database and Collection.

  1. In the Index Name field, enter `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

  2. In the Database and Collection section, find the `sample_mflix` database, and select the `movies` collection.

5

### Define an index on the `plot` field.

You can use the Visual Editor or the JSON Editor in the Atlas user interface
to create the index.

Visual Editor

JSON Editor

  1. Click Next.

  2. Click Refine Your Index.

  3. In the Index Configurations section, toggle to disable Dynamic Mapping.

  4. In the Field Mappings section, click

  5. Add Field to display the Add Field Mapping window.

  6. Select `plot` from the Field Name dropdown.

  7. Click the Data Type dropdown to specify the field type and the settings for the operator you want to use to run the query.

autocomplete

phrase

regex

wildcard

    1. Select Autocomplete from the dropdown to run the query using the autocomplete operator.

    2. Modify the default settings for the data type as shown below:

UI Field Name

|

Configuration  
  
|  
  
Max Grams

|

`15`  
  
Min Grams

|

`2`  
  
Tokenization

|

edgeGram  
  
Fold Diacritics

|

true  
  
To learn more about these settings, see How to Index Fields for
Autocompletion.

  8. Click Add to add the field to the list in Field Mappings section.

  9. Click Save Changes.

6

### Click Create Search Index.

7

### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

8

### Wait for the index to finish building.

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

## Run a Case-Sensitive Partial Match Query

* * *

➤ Use the **Select your language** drop-down menu on this page to set the
language of the examples in this section.

* * *

You can use the autocomplete, phrase, regex, and wildcard operators to run a
case-sensitive partial match query. This tutorial uses these operators to
search for movies whose plot contain the specified partial string. The query
uses the following pipeline stages:

  * `$search` stage to search the collection

  * `$limit` stage to limit the output to `5` results

  * `$project` stage to exclude all fields except `title` and `plot`

In this section, you will connect to your Atlas cluster and run the sample
query using the operator against the `plot` field in the `sample_mflix.movies`
collection.

MongoDB Shell

Compass

Go

Java (Sync)

Node.js

Python

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `sample_mflix` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_mflix  
      
  
MongoDB Shell

3

### Run the following Atlas Search query using the operator for which you
created the index.

The following query uses the operator to query the `plot` field of the
`sample_mflix.movies` collection. The query includes a:

  * `$limit` stage to limit the output to 5 results

  * `$project` stage to exclude all fields except `title` and `plot`

autocomplete

phrase

regex

wildcard

The query allows the following for matching the query string `new purchase` to
a word in the field:

  * Allows the words `new` and `purchase` to appear anywhere in the `plot` field.

  * Allows two character variation in the query string to match the query to a word in the field, but doesn't allow the first character in the query string to change.

  * Allows up to two hundred and fifty six similar terms to be considered.

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "autocomplete": {  
            "path": "plot",  
            "query": "new purchase",  
            "tokenOrder": "any",  
            "fuzzy": {  
              "maxEdits": 2,  
              "prefixLength": 1,  
              "maxExpansions": 256  
            }  
          },  
          "highlight": {  
             "path": "plot"  
          }  
        }  
      },  
      {  
        "$limit": 5  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1,  
          "plot": 1,  
          "highlights": { "$meta": "searchHighlights" }  
        }  
      }  
    ])  
  
MongoDB Shell

The preceding query returns the following results:

autocomplete

phrase

regex

wildcard

    
    
    1| [  
    |  
    2|   {  
    3|     plot: "A divorced woman and her diabetic daughter take refuge in their newly-purchased house's safe room, when three men break-in, searching for a missing fortune.",  
    4|     title: 'Panic Room',  
    5|     highlights: [  
    6|       {  
    7|         score: 4.364492893218994,  
    8|         path: 'plot',  
    9|         texts: [  
    10|           {  
    11|             value: 'A divorced woman and her diabetic daughter take refuge in their ',  
    12|             type: 'text'  
    13|           },  
    14|           { value: "newly-purchased house's safe", type: 'hit' },  
    15|           {  
    16|             value: ' room, when three men break-in, searching for a missing fortune.',  
    17|             type: 'text'  
    18|           }  
    19|         ]  
    20|       }  
    21|     ]  
    22|   },  
    23|   {  
    24|     plot: "A lonely writer develops an unlikely relationship with his newly purchased operating system that's designed to meet his every need.",  
    25|     title: 'Her',  
    26|     highlights: [  
    27|       {  
    28|         score: 4.198050022125244,  
    29|         path: 'plot',  
    30|         texts: [  
    31|           {  
    32|             value: 'A lonely writer develops an unlikely relationship with his ',  
    33|             type: 'text'  
    34|           },  
    35|           { value: 'newly purchased operating system', type: 'hit' },  
    36|           {  
    37|             value: " that's designed to meet his every ",  
    38|             type: 'text'  
    39|           },  
    40|           { value: 'need', type: 'hit' },  
    41|           { value: '.', type: 'text' }  
    42|         ]  
    43|       }  
    44|     ]  
    45|   },  
    46|   {  
    47|     plot: "A country boy becomes the head of a gang through the purchase of some lucky roses from an old lady. He and a singer at the gang's nightclub try to do a good deed for the old lady when her daughter comes to visit.",  
    48|     title: 'Miracles - Mr. Canton and Lady Rose',  
    49|     highlights: [  
    50|       {  
    51|         score: 2.0294458866119385,  
    52|         path: 'plot',  
    53|         texts: [  
    54|           {  
    55|             value: 'A country boy becomes the head of a gang through the ',  
    56|             type: 'text'  
    57|           },  
    58|           { value: 'purchase of some', type: 'hit' },  
    59|           { value: ' lucky roses from an old lady. ', type: 'text' }  
    60|         ]  
    61|       },  
    62|       {  
    63|         score: 0.9982474446296692,  
    64|         path: 'plot',  
    65|         texts: [  
    66|           { value: "He and a singer at the gang's ", type: 'text' },  
    67|           { value: 'nightclub try to', type: 'hit' },  
    68|           {  
    69|             value: ' do a good deed for the old lady when her daughter comes to visit.',  
    70|             type: 'text'  
    71|           }  
    72|         ]  
    73|       }  
    74|     ]  
    75|   },  
    76|   {  
    77|     plot: 'A psychologically troubled novelty supplier is nudged towards a romance with an English woman, all the while being extorted by a phone-sex line run by a crooked mattress salesman, and purchasing stunning amounts of pudding.',  
    78|     title: 'Punch-Drunk Love',  
    79|     highlights: [  
    80|       {  
    81|         score: 1.2451990842819214,  
    82|         path: 'plot',  
    83|         texts: [  
    84|           { value: 'A psychologically troubled ', type: 'text' },  
    85|           { value: 'novelty supplier is', type: 'hit' },  
    86|           { value: ' ', type: 'text' },  
    87|           { value: 'nudged towards a', type: 'hit' },  
    88|           {  
    89|             value: ' romance with an English woman, all the while being extorted by a phone-sex line run by a crooked mattress salesman, and ',  
    90|             type: 'text'  
    91|           },  
    92|           { value: 'purchasing stunning amounts', type: 'hit' },  
    93|           { value: ' of pudding.', type: 'text' }  
    94|         ]  
    95|       }  
    96|     ]  
    97|   },  
    98|   {  
    99|     plot: 'Jack Conrad is awaiting the death penalty in a corrupt Central American prison. He is "purchased" by a wealthy television producer and taken to a desolate island where he must fight to the death against nine other condemned killers from all corners of the world, with freedom going to the sole survivor.',  
    100|     title: 'The Condemned',  
    101|     highlights: [  
    102|       {  
    103|         score: 2.94378924369812,  
    104|         path: 'plot',  
    105|         texts: [  
    106|           { value: 'He is "', type: 'text' },  
    107|           { value: 'purchased" by a', type: 'hit' },  
    108|           {  
    109|             value: ' wealthy television producer and taken to a desolate island where he must fight to the death against ',  
    110|             type: 'text'  
    111|           },  
    112|           { value: 'nine other condemned', type: 'hit' },  
    113|           {  
    114|             value: ' killers from all corners of the world, with freedom going to the sole survivor.',  
    115|             type: 'text'  
    116|           }  
    117|         ]  
    118|       }  
    119|     ]  
    120|   }  
    121| ]  
  
MongoDB Shell

← How to Use Facets with Atlas SearchHow to Use Synonyms with Atlas Search →

