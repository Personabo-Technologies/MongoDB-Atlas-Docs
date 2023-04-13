Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Use Autocomplete with Atlas Search

Select your language

MongoDB Shell

On this page

  * Define an Index with Autocomplete
  * Run an Autocomplete Query
  * Continue Learning

This tutorial describes how to create an Atlas Search index that enables
autocomplete queries. In the following examples, the index enables
`autocomplete` operators to query the specified field values.

Both examples take you through the following steps:

  1. Set up an Atlas Search index with autocomplete data type for the `sample_mflix.movies` collection.

  2. Run Atlas Search queries against the specified fields in the `sample_mflix.movies` collection for an inputted sequence of characters.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Define an Index with Autocomplete

You can use the Atlas Search `autocomplete` type to index text values in
string fields for autocompletion. You can configure an `autocomplete` type to
satisfy a variety of use cases. To learn more about the configuration options
available for the `autocomplete` type, such as tokenization strategy and
diacritic folding, see Configure `autocomplete` Field Properties. You can
query fields indexed as `autocomplete` type only using the autocomplete
operator.

In this section, you will create an Atlas Search index that indexes the
`title` and `plot` fields for autocompletion using the `edgeGram` tokenization
strategy.

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

### Specify an index definition with the `autocomplete` field type.

You can use the Visual Editor or the JSON Editor in the Atlas user interface
to create the index.

Visual Editor

JSON Editor

  1. Click Next.

  2. Click Refine Your Index.

  3. Click Add Field in the Field Mappings section.

  4. Configure the following field for autocompletion:

UI Field Name

|

Configuration  
  
|  
  
Field Name

|

Enter `title`.  
  
Data Type

|

Select `Autocomplete`.  
  
  5. Review the following default settings:

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
  
  6. Click Add.

  7. Repeat steps **c** through **g** for the `plot` field.

  8. Click Save Changes.

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

## Run an Autocomplete Query

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
example on this page.

* * *

The autocomplete operator performs a search for a word or phrase that contains
a sequence of characters from an incomplete input string. You can use the
`autocomplete` operator with search-as-you-type applications to predict words
with increasing accuracy as characters are entered in your application's
search field. `autocomplete` returns results that contain predicted words
based on the tokenization strategy specified in the index definition for
autocompletion. The fields that you intend to query with the `autocomplete`
operator must be indexed with the How to Index Fields for Autocompletion data
type in the collection's index definition.

## Note

Atlas Search might return inaccurate results for queries with more than three
words in a single string.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

Basic Example

Advanced Example

In this section, you will connect to your Atlas cluster and run the sample
queries against the `title` field in the `sample_mflix.movies` collection
using the `autocomplete` operator. This sample query uses a sequence of
characters to find movie titles that include words that begin with the input
character string.

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

### Run an Atlas Search query with the `autocomplete` operator on the `movies`
collection.

The following query searches for movies with the characters `ger` in the
`title` field. The query includes the `$limit` stage to limit the output to 20
results and the `$project` stage to exclude all fields except `title`.

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "autocomplete": {  
            "path": "title",  
            "query": "ger"  
          }  
        }  
      },  
      {  
        $limit: 20  
      },  
      {  
        $project: {  
          "_id": 0,  
          "title": 1  
        }  
      }  
    ])  
  
MongoDB Shell

This query returns the following results:

    
    
    1| { title: "Gertie the Dinosaur" },  
    |  
    2| { title: "Germany Year Zero" },  
    3| { title: "Germany in Autumn" },  
    4| { title: "Germany Pale Mother" },  
    5| { title: "Gerhard Richter - Painting" },  
    6| { title: "Geronimo: An American Legend" },  
    7| { title: "How to Live in the German Federal Republic" },  
    8| { title: "Geri's Game" },  
    9| { title: "The Gerson Miracle" },  
    10| { title: "The German Doctor" },  
    11| { title: "From Caligari to Hitler: German Cinema in the Age of the Masse"},  
    12| { title: "From Caligari to Hitler: German Cinema in the Age of the Masses"},  
    13| { title: "Gèraldine" },  
    14| { title: "Gervaise" },  
    15| { title: "Gertrud" },  
    16| { title: "Germinal" },  
    17| { title: "Gerry" },  
    18| { title: "Gerontophilia" },  
    19| { title: "Pionery-geroi" },  
    20| { title: "The Good German" }  
  
MongoDB Shell

In these results, the characters `ger` appear at the beginning of a word in
all the titles. Atlas Search returns results that begin with the specified
query string because the `title` field is indexed using the `edgeGram`
tokenization strategy. Atlas Search includes `Gèraldine` and `Rece do gèry` in
the results because we set `foldDiacritics` to `true`.

## Continue Learning

Follow along with this video tutorial walk-through that demonstrates how to
use the Atlas Search autocomplete operator and JavaScript to build a frontend
form element that suggests data to the user.

 _Duration: 30 minutes_

← Atlas Search TutorialsHow to Run Atlas Search Compound Queries with Weighted
Fields →

