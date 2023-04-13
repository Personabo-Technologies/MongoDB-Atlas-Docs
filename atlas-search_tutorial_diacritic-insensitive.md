Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Define a Custom Analyzer and Run an Atlas Search Diacritic-
Insensitive Query

Select your language

MongoDB Shell

On this page

  * Create the Atlas Search Index
  * Search the Collection

This tutorial describes how to create an index that uses a custom analyzer and
run a diacritic-insensitive query against the `sample_mflix.movies`
collection. It takes you through the following steps:

  1. Set up an Atlas Search index on the `title` and `genres` fields in the `sample_mflix.movies` collection.

  2. Run an Atlas Search compound query against the `title` and `genres` fields in the `sample_mflix.movies` collection using the wildcard and text operators.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Create the Atlas Search Index

In this section, you will create an Atlas Search index on the `title` and
`genres` fields in the `sample_mflix.movies` collection.

1

### Navigate to the Atlas Search page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

### Click Create Index.

3

### Select JSON editor for the Configuration Method and click Next.

4

### Enter the Index Name, and set the Database and Collection.

  1. In the Index Name field, enter `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

  2. In the Database and Collection section, find the `sample_mflix` database, and select the `movies` collection.

5

### Specify an index definition.

Use the JSON Editor in the Atlas user interface to create the index.

  1. Replace the default definition with the following:

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "fields": {  
    4|       "genres": {  
    5|         "type": "string"  
    6|       },  
    7|       "title": {  
    8|         "analyzer": "diacriticFolder",  
    9|         "type": "string"  
    10|       }  
    11|     }  
    12|   },  
    13|   "analyzers": [{  
    14|     "charFilters": [],  
    15|     "name": "diacriticFolder",  
    16|     "tokenizer": {  
    17|       "type": "keyword"  
    18|     },  
    19|     "tokenFilters": [{  
    20|       "type": "icuFolding"  
    21|     }]  
    22|   }]  
    23| }  
  
This index definition for the `genres` and `title` fields specifies a custom
analyzer, `diacriticFolder`, using the following:

  * keyword tokenizer that tokenizes the entire input as a single token.

  * icuFolding token filter that applies character foldings such as accent removal and case folding.

The index definition specifies a string type for the `genres` and `title`
fields. It also applies the custom analyzer named `diacriticFolder` on the
`title` field.

  1. Click Next.

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

## Search the Collection

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
example in this section.

* * *

You can use the compound operator to combine two or more operators into a
single query. The sample query in this section uses the compound operator to
query the `title` and `genres` fields in the `movies` collection using
multiple operators.

In this section, connect to your Atlas cluster and run the sample query
against the `sample_mflix.movies` collection using the `compound` operator.

MongoDB Shell

Compass

C#

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

### Run an Atlas Search diacritic-insensitive query.

This query uses the `$search` stage to query the collection using the
`compound` operator. The `compound` operator uses the following clauses:

  * `must` clause to search for movie titles that begin with the term `alle` using the wildcard operator

  * `should` clause to specify preference for the `Drama` genre using the text operator

The query uses the `$project` stage to:

  * Exclude all fields except `title` and `genres`

  * Add a field named `score`

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     "$search" : {  
    4|       "compound" : {  
    5|         "must": [{  
    6|             "wildcard" : {  
    7|               "query" : "alle*",  
    8|               "path": "title",  
    9|               "allowAnalyzedField": true  
    10|         }  
    11|         }],  
    12|         "should": [{  
    13|           "text": {  
    14|             "query" : "Drama",  
    15|             "path" : "genres"  
    16|           }  
    17|         }]  
    18|       }  
    19|     }  
    20|   },  
    21|   {  
    22|     "$project" : {  
    23|       "_id" : 0,  
    24|       "title" : 1,  
    25|       "genres" : 1,  
    26|       "score" : { "$meta": "searchScore" }  
    27|     }  
    28|   }  
    29| ])  
  
MongoDB Shell

HIDE OUTPUT

    
    
    {  
      
      genres: [ 'Drama', 'Thriller' ],  
      title: 'Allèluia',  
      score: 1.249049425125122  
    },  
    {  
      genres: [ 'Drama', 'Family', 'Sport' ],  
      title: 'Alley Cats Strike',  
      score: 1.2084882259368896  
    },  
    {  
      genres: [ 'Drama', 'Romance', 'Sci-Fi' ],  
      title: 'Allegro',  
      score: 1.179288625717163  
    },  
    {  
      genres: [ 'Animation', 'Comedy', 'Fantasy' ],  
      title: 'Allegro non troppo',  
      score: 1  
    },  
    {  
      genres: [ 'Comedy' ],  
      title: 'Allez, Eddy!',  
      score: 1  
    }  
  
The first document in the result includes diacritics in the `title` field
because the `diacriticFolder` custom analyzer we used on the `title` field
applied character folding on its values. Atlas Search returns documents with
titles that begin with the query term `alle` because we used the keyword
tokenizer, which tokenizes entire strings (or phrases) as a single token.

Alternatively, you can specify the standard tokenizer instead of the keyword
tokenizer in the custom analyzer used on the title field. For the standard
tokenizer, the Atlas Search results would contain documents with titles that
begin or appear anywhere at the beginning of the word for the query term
`alle` such as "Desde allè". To test this, edit your index definition to
replace the `keyword` tokenizer on line 17 with `standard` tokenizer, save the
index definition, and run the sample query.

← How to Run Multilingual Atlas Search QueriesHow to Sort Your Atlas Search
Results for Your Perfomance Needs →

