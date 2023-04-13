Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run Atlas Search Compound Queries with Weighted Fields

Select your language

MongoDB Shell

On this page

  * Create the Atlas Search Index With Dynamic Mapping
  * Run a Compound Query
  * Continue Learning

This tutorial describes how to create an index with dynamic mapping on the
`sample_mflix.movies` collection. It shows how to run compound queries against
the `year` field and alter the score using `constant`, `function`, and
`boost`. It takes you through the following steps:

  1. Set up an Atlas Search index with dynamic mapping for the `sample_mflix.movies` collection.

  2. Run Atlas Search queries against the `year` field in the `sample_mflix.movies` collection and alter the score using specific a word in the `title` field.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Create the Atlas Search Index With Dynamic Mapping

In this section, you will create an Atlas Search index that uses dynamic
mapping to index the fields in the `sample_mflix.movies` collection.

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

### Specify an index definition.

You can create an Atlas Search index that uses dynamic mappings through the
Visual Editor or JSON Editor in the Atlas User Interface. The following index
definition dynamically indexes the fields of supported types in the `movies`
collection.

#### Visual Editor

  1. Click Next.

  2. Review the `"default"` index definition for the `movies` collection.

#### JSON Editor

  1. Click Next.

  2. Review the index definition.

Your index definition should look similar to the following:

    
        {  
      
      "mappings": {  
        "dynamic": true  
      }  
    }  
  
The above index definition dynamically indexes the fields of supported types
in each document in the `movies` collection.

  3. Click Next.

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

## Run a Compound Query

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
examples in this section.

* * *

You can use the compound operator to combine two or more operators into a
single query. Every document that Atlas Search returns for your query is
assigned a score based on relevance, in order from highest score to lowest. In
this section, you will connect to your Atlas cluster and run the sample
queries using the compound operator against the `title` and `year` fields in
the `sample_mflix.movies` collection. The sample queries use custom scoring to
alter the relevance score returned by Atlas Search.

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

### Run the following Atlas Search queries with the `compound` operator on the
`movies` collection.

The following examples use the `compound` operator with subqueries to search
for movies between the years `2013` to `2015` with the term `snow` in the
`title` field.

Constant

Boost Single

Boost Multiple

Function Score

This query uses the following pipeline stages:

  * `$search` to query the collection. The query:

    * Uses the following `compound` operator clauses:

      * `filter` clause with the range operator to search for movies between the years `2013` to `2015`.

      * `should` clause with the text operator to query for the term `snow` in the `title` field and alter the `score` with the `constant` option. The `constant` option replaces all score results for the search term with `5`.

    * Specifies the highlight option to return snippets of text from the `title` field that match the query. The snippets contain matching text specified with `type: 'hit'`, and adjacent text specified with `type: 'text'`.

  * `$limit` stage to limit the output to `10` results.

  * `$project` stage to:

    * Exclude all fields except `title` and `year`

    * Add a `score` field

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "compound": {  
            "filter": [{  
              "range": {  
                "path": "year",  
                "gte": 2013,  
                "lte": 2015  
              }  
            }],  
            "should": [{  
              "text": {  
                "query": "snow",  
                "path": "title",  
                "score": {"constant": {"value": 5}}  
              }  
            }]  
          },  
          "highlight": {  
            "path": "title"  
          }  
        }  
      },  
      {  
        "$limit": 10  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1,  
          "year": 1,  
          "score": { "$meta": "searchScore" },  
          "highlights": { "$meta": "searchHighlights" }  
        }  
      }  
    ])  
  
MongoDB Shell

Atlas Search returns the following results for `constant`:

    
    
     [  
      
      {  
        title: 'Snow in Paradise',  
        year: 2014,  
        score: 5,  
        highlights: [  
          {  
            score: 1.382846713066101,  
            path: 'title',  
            texts: [  
              { value: 'Snow', type: 'hit' },  
              { value: ' in Paradise', type: 'text' }  
            ]  
          }  
        ]  
      },  
      {  
        title: 'Dead Snow 2: Red vs. Dead',  
        year: 2014,  
        score: 5,  
        highlights: [  
          {  
            score: 1.3924485445022583,  
            path: 'title',  
            texts: [  
              { value: 'Dead ', type: 'text' },  
              { value: 'Snow', type: 'hit' },  
              { value: ' 2: Red vs. ', type: 'text' }  
            ]  
          }  
        ]  
      },  
      {  
        title: 'The Snow White Murder Case',  
        year: 2014,  
        score: 5,  
        highlights: [  
          {  
            score: 1.3525336980819702,  
            path: 'title',  
            texts: [  
              { value: 'The ', type: 'text' },  
              { value: 'Snow', type: 'hit' },  
              { value: ' White Murder Case', type: 'text' }  
            ]  
          }  
        ]  
      },  
      {  
        title: 'Snow on the Blades',  
        year: 2014,  
        score: 5,  
        highlights: [  
          {  
            score: 1.3766303062438965,  
            path: 'title',  
            texts: [  
              { value: 'Snow', type: 'hit' },  
              { value: ' on the Blades', type: 'text' }  
            ]  
          }  
        ]  
      },  
      { year: 2013, title: 'The Secret Life of Walter Mitty', score: 0, highlights: [] },  
      { title: 'Jurassic World', year: 2015, score: 0, highlights: [] },  
      { title: 'Action Jackson', year: 2014, score: 0, highlights: [] },  
      { year: 2013, title: 'In Secret', score: 0, highlights: [] },  
      { title: 'The Stanford Prison Experiment', year: 2015, score: 0, highlights: [] },  
      { year: 2014, title: 'The Giver', score: 0, highlights: [] }  
    ]  
  
The first four documents in the results have a higher score because the
`should` clause in the query specifies a preference for documents with `snow`
in the title. The `should` clause also alters the score for the query term
`snow` using the `constant` option.

## Continue Learning

To learn more about compound queries using Atlas Search, take Unit 9 of the
Intro To MongoDB Course on MongoDB University. The 1.5 hour unit includes an
overview of Atlas Search and lessons on creating Atlas Search indexes, running
`$search` queries using compound operators, and grouping results using facet.

← How to Use Autocomplete with Atlas SearchHow to Run Atlas Search Queries
Against Objects in Arrays →

