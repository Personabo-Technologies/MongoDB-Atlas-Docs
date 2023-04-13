Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update $text Queries with Atlas Search for Improved Search Performance

Share Feedback

On this page

  * Atlas Search Feature Advantages
  * Examples
  * Learn More

If your queries rely heavily on the `$text` aggregation pipeline stage, you
can modify these queries to use `$search` instead to improve both the
flexibility and performance of these queries.

## Atlas Search Feature Advantages

The `$search` aggregation stage provides the following features which are
either not available through the `$text` operator, available but less
performant, or available only with significant implementation work by the
user:

  * Language awareness

  * Case-insensitive and diacritic-insensitive search

  * Result text highlighting

  * Geospatial-aware queries

  * Character and word autocompletion with different tokenization strategies

  * Fuzzy matching

  * Filtering on 10 or more strings with the compound operator

  * Customizable relevance scoring and sorting

  * Single compound indexes on arrays

  * Synonym search

  * Bucketing for faceted navigation

  * Custom analyzers

  * Partial matching

  * Phrase queries

## Examples

### Create the Indexes

The examples in the following sections use queries against the
`sample_mflix.movies` collection in the sample data to illustrate the
improvements to flexibility and performance that Atlas Search offers over
`$text`. You can run the queries from both examples using the following
indexes:

Text Index

|

Atlas Search Index  
  
|  
      
    
    | db.movies.createIndex(  
      
      {  
        genres: "text",  
        plot: "text",  
        year: -1  
      }  
    )  
      
    
    | {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "genres": {  
            "type": "string"  
          },  
          "plot": {  
            "type": "string"  
          },  
          "year": {  
            "type": "number"  
          }  
        }  
      }  
    }  
  
Either index definition will index the `genres` and `plot` fields as text, and
the `year` field as numeric. For instructions on creating `$text` indexes, see
Create Text Index. For instructions on creating Atlas Search indexes, see
Create an Atlas Search Index.

### Improve Flexibility of Full-Text Queries with Atlas Search

You can update your `$text`-based queries to use `$search` for greater
flexibility and convenience. In this example, you will query the
`sample_mflix.movies` collection in the sample data to retrieve entries with
the word 'poet' in the `plot` field, sorted in ascending order by year.

The index definitions laid out in the previous section illustrate one of the
flexibility enhancements of `$search`: in order to create the `$text` index on
`sample_mflix.movies`, you must first delete any existing text index on the
sample data, as MongoDB supports only a single text index per collection.

In contrast, you can create multiple Atlas Search indexes for a single
collection, allowing your applications to leverage distinct full text queries
in parallel.

The following queries return the five most recent movies with 'poet' in the
`plot` field, showing their titles, genres, plots, and years of release.

Regex Index

|

Atlas Search Index  
  
|  
      
    
    | db.movies.find(  
      
       {  
         $text: { $search: "poet" }  
       },  
       {  
         _id: 0,  
         title: 1,  
         genres: 1,  
         plot: 1,  
         year: 1  
       }  
    ).limit(5)  
      
    
    | db.movies.aggregate([  
      
       {  
         "$search": {  
           "text": {  
             "path": "plot",  
             "query": "poet"  
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
           "genres": 1,  
           "plot": 1,  
           "year": 1,  
         }  
       }  
    ])  
  
Both of these queries return the following results:

    
    
    {  
      
     plot: `It's the story of the murder of a poet, a man, a great film director: Pier Paolo Pasolini. The story begin with the arrest of "Pelosi", a young man then accused of the murder of the poet. ...`,  
     genres: [ 'Crime', 'Drama' ],  
     title: 'Who Killed Pasolini?',  
     year: 1995  
    },  
    {  
     plot: 'Friendship and betrayal between two poets during the French Revolution.',  
     genres: [ 'Biography', 'Drama' ],  
     title: 'Pandaemonium',  
     year: 2000  
    },  
    {  
     year: 2003,  
     plot: 'Story of the relationship between the poets Ted Hughes and Sylvia Plath.',  
     genres: [ 'Biography', 'Drama', 'Romance' ],  
     title: 'Sylvia'  
    },  
    {  
     year: 2003,  
     plot: 'Story of the relationship between the poets Ted Hughes and Sylvia Plath.',  
     genres: [ 'Biography', 'Drama', 'Romance' ],  
     title: 'Sylvia'  
    },  
    {  
     plot: 'A love-struck Italian poet is stuck in Iraq at the onset of an American invasion.',  
     genres: [ 'Comedy', 'Drama', 'Romance' ],  
     title: 'The Tiger and the Snow',  
     year: 2005  
    }  
  
Unique to Atlas Search, you can add highlights to the results, displaying
matches in the contexts in which they were found. To do so, replace the Atlas
Search query above with the following:

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "text": {  
    5|         "path": "plot",  
    6|         "query": "poet"  
    7|       },  
    8|       "highlight": {  
    9|         "path": "plot"  
    10|       }  
    11|     }  
    12|   },  
    13|   {  
    14|     "$limit": 1  
    15|   },  
    16|   {  
    17|     "$project": {  
    18|       "_id": 0,  
    19|       "title": 1,  
    20|       "genres": 1,  
    21|       "plot": 1,  
    22|       "year": 1,  
    23|       "highlights": { "$meta": "searchHighlights" }  
    24|     }  
    25|   }  
    26| ])  
  
The results of the above query include the `highlights` field, which contains
both the context in which all matches occurred, and relevance scores for each.
For example, the following shows the `highlights` field for the first document
in the `$search` results.

    
    
    {  
      
      plot: `It's the story of the murder of a poet, a man, a great film director: Pier Paolo Pasolini. The story begin with the arrest of "Pelosi", a young man then accused of the murder of the poet. ...`,  
      genres: [ 'Crime', 'Drama' ],  
      title: 'Who Killed Pasolini?',  
      year: 1995,  
      highlights: [  
        {  
          score: 1.0902210474014282,  
          path: 'plot',  
          texts: [  
            { value: "It's the story of the murder of a ", type: 'text' },  
            { value: 'poet', type: 'hit' },  
            {  
              value: ', a man, a great film director: Pier Paolo Pasolini. ',  
              type: 'text'  
            }  
          ]  
        },  
        {  
          score: 1.0202842950820923,  
          path: 'plot',  
          texts: [  
            {  
              value: 'The story begin with the arrest of "Pelosi", a young man then accused of the murder of the ',  
              type: 'text'  
            },  
            { value: 'poet', type: 'hit' },  
            { value: '. ...', type: 'text' }  
          ]  
        }  
      ]  
    }  
  
### Improve Performance of Queries using Atlas Search

In addition to greater flexibility and convenience, Atlas Search provides
significant performance advantages over analogous `$text` queries. Consider a
query against the `sample_mflix.movies` collection to retrieve movies released
between 2000 and 2010, in the comedy genre, with 'poet' in the `plot` field.

Run the following queries:

Text Index

|

Atlas Search Index  
  
|  
      
    
    | db.movies.aggregate([  
      
      {  
        $match: {  
          year: {$gte: 2000, $lte: 2010},  
          $text: { $search: "poet" },  
          genres : { $eq: "Comedy" }  
        }  
      },  
      { "$sort": { "year": 1 } },  
      {  
        "$limit": 3  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1,  
          "genres": 1,  
          "plot": 1,  
          "year": 1  
        },  
      
      }  
    ])  
      
    
    | db.movies.aggregate([  
      
      {  
        "$search": {  
          "compound": {  
            "filter": [{  
              "range": {  
                "gte": 2000,  
                "lte": 2010,  
                "path": "year"  
              }  
            },  
            {  
              "text": {  
                "path": "plot",  
                "query": "poet"  
              }  
            },  
            {  
              "text": {  
                "path": "genres",  
                "query": "comedy"  
              }  
            }]  
          }  
        }  
      },  
      { "$sort": { "year": 1 } },  
      {  
        "$limit": 3  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1,  
          "genres": 1,  
          "plot": 1,  
          "year": 1  
        }  
      }  
    ])  
  
Both of these queries will return the following three documents.

    
    
       {  
      
      year: 2000,  
      plot: 'A film poem inspired by the Peruvian poet Cèsar Vallejo. A story about our need for love, our confusion, greatness and smallness and, most of all, our vulnerability. It is a story with many...',  
      genres: [ 'Comedy', 'Drama' ],  
      title: 'Songs from the Second Floor'  
    },  
    {  
      plot: 'When his mother, who has sheltered him his entire 40 years, dies, Elling, a sensitive, would-be poet, is sent to live in a state institution. There he meets Kjell Bjarne, a gentle giant and...',  
      genres: [ 'Comedy', 'Drama' ],  
      title: 'Elling',  
      year: 2001  
    },  
    {  
      plot: 'Heart-broken after several affairs, a woman finds herself torn between a Poet and a TV Host.',  
      genres: [ 'Comedy', 'Romance', 'Drama' ],  
      title: 'Easy',  
      year: 2003  
    }  
  
Although `$text` is adequate for simple, narrow searches such as this, as the
size of the datasets and breadth of your queries increases, the performance
advantages of `$search` will significantly improve the responsiveness of your
applications. We recommend that you use an Atlas Search query through the
$search aggregation pipeline stage.

## Learn More

  * To learn more about Atlas Search queries, see Create and Run Atlas Search Queries.

  * MongoDB University offers a free course on optimizing MongoDB Performance. To learn more, see M201: MongoDB Performance.

← Atlas Search Best PracticesUse Atlas Search for Full-Text Search Queries →

