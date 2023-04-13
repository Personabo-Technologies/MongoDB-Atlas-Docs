Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Highlight Search Terms in Results

Share Feedback

On this page

  * Syntax
  * Options
  * Output
  * Limitations
  * Examples
  * Basic Example
  * Advanced Example
  * Multi-Field Example
  * Wildcard Example
  * Autocomplete Example
  * Compound Example

The Atlas Search `highlight` option adds fields to the result set that display
search terms in their original context. You can use it in conjunction with all
$search operators to display search terms as they appear in the returned
documents, along with the adjacent text content (if any). `highlight` results
are returned as part of the `$meta` field.

## Tip

### See also:

Stemming

## Syntax

`highlight` has the following syntax:

    
    
    {  
      
      $search: {  
        "index": "<index name>", // optional, defaults to "default"  
        "<operator>": { // such as "text", "compound", or "phrase"  
          <operator-specification>  
        },  
        "highlight": {  
          "path": "<field-to-search>",  
          "maxCharsToExamine": "<number-of-chars-to-examine>", // optional, defaults to 500,000  
          "maxNumPassages": "<number-of-passages>" // optional, defaults to 5  
        }  
      }  
    },  
    {  
      $project: {  
        "highlights": { "$meta": "searchHighlights" }  
      }  
    }  
  
## Options

Field

|

Type

|

Description

|

Required?  
  
|||  
  
`path`

|

string

|

Document field to search. The `path` field may contain:

  * A string

  * An array of strings

  * A multi analyzer specification

  * An array containing a combination of strings and multi analyzer specifications

  * A wildcard character `*`

See Construct a Query Path for more information.

|

yes  
  
`maxCharsToExamine`

|

int

|

Maximum number of characters to examine on a document when performing
highlighting for a field. If omitted, defaults to `500,000`, which means that
Atlas Search only examines the first 500,000 characters in the search field in
each document for highlighting.

|

no  
  
`maxNumPassages`

|

int

|

Number of high-scoring passages to return per document in the `highlights`
results for each field. A passage is roughly the length of a sentence. If
omitted, defaults to 5, which means that for each document, Atlas Search
returns the top 5 highest-scoring passages that match the search text.

|

no  
  
The `"$meta": "searchHighlights"` field contains the highlighted results. That
field isn't part of the original document, so it is necessary to use a
$project pipeline stage to add it to the query output.

## Output

The `highlights` field is an array containing the following output fields:

Field

|

Type

|

Description  
  
||  
  
`path`

|

string

|

Document field which returned a match.  
  
`texts`

|

array of documents

|

Each search match returns one or more objects, containing the matching text
and the surrounding text (if any).  
  
`texts.value`

|

string

|

Text from the field which returned a match.  
  
`texts.type`

|

string

|

Type of result. Value can be one of the following:

  * `hit` \- The results contain the term that matched the query.

  * `text` \- The results contain the text content adjacent to the matching term.

  
  
`score`

|

float

|

Score assigned to the matching result. The `highlights` score is a measure of
the relevance of the `highlights` object to the query. If multiple
`highlights` objects are returned, the most relevant `highlights` object has
the highest score.  
  
## Limitations

You can't use the Atlas Search `highlight` option in conjunction with the
embeddedDocument operator.

## Examples

The examples on this page use a collection called `fruit` that contains the
following documents:

    
    
    {  
      
      "_id" : 1,  
      "type" : "fruit",  
      "summary" : "Apple varieties",  
      "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp. The most popular varieties are McIntosh, Gala, and Granny Smith.",  
      "category": "organic"  
    },  
    {  
      "_id" : 2,  
      "type" : "fruit",  
      "summary" : "Banana",  
      "description" : "Bananas are usually sold in bunches of five or six.",  
      "category": "nonorganic"  
    },  
    {  
      "_id" : 3,  
      "type" : "fruit",  
      "summary" : "Pear varieties",  
      "description" : "Bosc and Bartlett are the most common varieties of pears.",  
      "category": "nonorganic"  
    }  
  
The `fruit` collection also has an index definition that uses the english
analyzer and dynamic field mappings.

    
    
    {  
      
      "analyzer": "lucene.english",  
      "searchAnalyzer": "lucene.english",  
      "mappings": {  
        "dynamic": true  
      }  
    }  
  
## Note

One useful aspect of highlighting is that it reveals the original text
returned by the search query, which may not be exactly the same as the search
term. For example, if you use a language-specific analyzer, your text searches
return all the stemmed variations of your search terms.

Another useful aspect of highlighting is that it can be used to highlight any
field, inside or outside of the query `path`. For example, when you search for
a term, you can perform highlighting for the query term on the query field and
any other fields that you specify using the `highlight` option. To learn more,
see Multi-Field Example.

### Basic Example

The following query searches for `variety` and `bunch` in the `description`
field of the `fruit` collection, with the `highlight` option enabled.

The $project pipeline stage restricts the output to the `description` field
and adds a new field called `highlights`, which contains highlighting
information.

    
    
    db.fruit.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "path": "description",  
            "query": ["variety", "bunch"]  
          },  
          "highlight": {  
            "path": "description"  
          }  
        }  
      },  
      {  
        $project: {  
          "description": 1,  
          "_id": 0,  
          "highlights": { "$meta": "searchHighlights" }  
        }  
      }  
    ])  
  
The query returns the following results:

    
    
    {  
      
      "description" : "Bananas are usually sold in bunches of five or six. ",  
      "highlights" : [  
        {  
          "path" : "description",  
          "texts" : [  
            {  
              "value" : "Bananas are usually sold in ",  
              "type" : "text"  
            },  
            {  
              "value" : "bunches",  
              "type" : "hit"  
            },  
            {  
              "value" : " of five or six. ",  
              "type" : "text"  
            }  
          ],  
          "score" : 1.2841906547546387  
        }  
      ]  
    }  
    {  
      "description" : "Bosc and Bartlett are the most common varieties of pears.",  
      "highlights" : [  
        {  
          "path" : "description",  
          "texts" : [  
            {  
              "value" : "Bosc and Bartlett are the most common ",  
              "type" : "text"  
            },  
            {  
              "value" : "varieties",  
              "type" : "hit"  
            },  
            {  
              "value" : " of pears.",  
              "type" : "text"  
            }  
          ],  
          "score" : 1.2691514492034912  
        }  
      ]  
    }  
    {  
      "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp. The most popular varieties are McIntosh, Gala, and Granny Smith. ",  
      "highlights" : [  
        {  
          "path" : "description",  
          "texts" : [  
            {  
              "value" : "Apples come in several ",  
              "type" : "text"  
            },  
            {  
              "value" : "varieties",  
              "type" : "hit"  
            },  
            {  
              "value" : ", including Fuji, Granny Smith, and Honeycrisp. ",  
              "type" : "text"  
            }  
          ],  
          "score" : 1.0330637693405151  
        },  
        {  
          "path" : "description",  
          "texts" : [  
            {  
              "value" : "The most popular ",  
              "type" : "text"  
            },  
            {  
              "value" : "varieties",  
              "type" : "hit"  
            },  
            {  
              "value" : " are McIntosh, Gala, and Granny Smith. ",  
              "type" : "text"  
            }  
          ],  
          "score" : 1.0940992832183838  
        }  
      ]  
    }  
  
The search term `bunch` returns a match on the document with `_id: 2`, because
the `description` field contains the word `bunches`. The search term `variety`
returns a match on the documents with `_id: 3` and `_id: 1`, because the
`description` field contains the word `varieties`.

### Advanced Example

The following query searches for `variety` and `bunch` in the `description`
field of the `fruit` collection, with the `highlight` option enabled, maximum
number of characters to examine set to `40`, and only `1` high-scoring passage
to return per document.

The $project pipeline stage restricts the output to the `description` field
and adds a new field called `highlights`, which contains highlighting
information.

    
    
    db.fruit.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "path": "description",  
            "query": ["variety", "bunch"]  
          },  
          "highlight": {  
            "path": "description",  
            "maxNumPassages": 1,  
            "maxCharsToExamine": 40  
          }  
        }  
      },  
      {  
        $project: {  
          "description": 1,  
          "_id": 0,  
          "highlights": { "$meta": "searchHighlights" }  
        }  
      }  
    ])  
  
The query returns the following results:

    
    
    {  
      
      "description" : "Bananas are usually sold in bunches of five or six. ",  
      "highlights" : [  
        {  
          "path" : "description",  
          "texts" : [  
            {  
              "value" : "Bananas are usually sold in ",  
              "type" : "text"  
            },  
            {  
              "value" : "bunches",  
              "type" : "hit"  
            },  
            {  
              "value" : " of f",  
              "type" : "text"  
            }  
          ],  
          "score" : 1.313065767288208  
        }  
      ]  
    }  
    {  
      "description" : "Bosc and Bartlett are the most common varieties of pears.",  
      "highlights" : [ ]  
    }  
    {  
      "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp. The most popular varieties are McIntosh, Gala, and Granny Smith.",  
      "highlights" : [  
        {  
          "path" : "description",  
          "texts" : [  
            {  
              "value" : "Apples come in several ",  
              "type" : "text"  
            },  
            {  
              "value" : "varieties",  
              "type" : "hit"  
            },  
            {  
              "value" : ", includ",  
              "type" : "text"  
            }  
          ],  
          "score" : 0.9093900918960571  
        }  
      ]  
    }  
  
The second document in the above results contains an empty `highlights` array
even though the search field contains the search term `varieties`, because
Atlas Search only examined `40` characters for highlighting. Similarly, the
word `includ` is truncated because Atlas Search only examined `40` characters
in the search field for highlighting. In the third document, although multiple
passages contain the search term, Atlas Search returns only one passage in the
`highlights` results because the query required only `1` passage per document
in the `highlights` results.

### Multi-Field Example

The following query searches for `varieties` in the `description` field of the
`fruit` collection, with the `highlight` option enabled for both the
`description` and `summary` fields.

The $project pipeline stage adds a new field called `highlights`, which
contains highlighting information for the query term across all fields in the
`highlight` option.

    
    
    db.fruit.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "path": "description",  
            "query": "varieties"  
          },  
          "highlight": {  
            "path": ["description", "summary" ]  
          }  
        }  
      },  
      {  
        $project: {  
          "description": 1,  
          "summary": 1,  
          "_id": 0,  
          "highlights": { "$meta": "searchHighlights" }  
        }  
      }  
    ])  
  
The query returns the following results:

    
    
    {  
      
      "summary" : "Pear varieties",  
      "description" : "Bosc and Bartlett are the most common varieties of pears.",  
      "highlights" : [  
        {  
          "path" : "summary",  
          "texts" : [  
            {  
              "value" : "Pear ",  
              "type" : "text"  
            },  
            {  
              "value" : "varieties",  
              "type" : "hit"  
            }  
          ],  
          "score" : 1.3891443014144897 },  
        {  
          "path" : "description",  
          "texts" : [  
            {  
              "value" : "Bosc and Bartlett are the most common ",  
              "type" : "text"  
            },  
            {  
              "value" : "varieties",  
              "type" : "hit"  
            },  
            {  
              "value" : " of pears.",  
              "type" : "text"  
            }  
          ],  
          "score" : 1.2691514492034912  
        }  
      ]  
    }  
    {  
      "summary" : "Apple varieties",  
      "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp. The most popular varieties are McIntosh, Gala, and Granny Smith.",  
      "highlights" : [  
        {  
          "path" : "summary",  
          "texts" : [  
            {  
              "value" : "Apple ",  
              "type" : "text"  
            },  
            {  
              "value" : "varieties",  
              "type" : "hit"  
            }  
          ],  
          "score" : 1.3859853744506836  
        },  
        {  
          "path" : "description",  
          "texts" : [  
            {  
              "value" : "Apples come in several ",  
              "type" : "text"  
            },  
            {  
              "value" : "varieties",  
              "type" : "hit"  
            },  
            {  
              "value" : ", including Fuji, Granny Smith, and Honeycrisp. ",  
              "type" : "text"  
            }  
          ],  
          "score" : 1.0330637693405151  
        },  
        {  
          "path" : "description",  
          "texts" : [  
            {  
              "value" : "The most popular ",  
              "type" : "text"  
            },  
            {  
              "value" : "varieties",  
              "type" : "hit"  
            },  
            {  
              "value" : " are McIntosh, Gala, and Granny Smith.",  
              "type" : "text"  
            }  
          ],  
          "score" : 1.0940992832183838  
        }  
      ]  
    }  
  
The search term `varieties` returns a match on documents with `_id: 1` and
`_id: 3` because the query field `description` in both documents contains the
query term `varieties`. In addition, the `highlights` array includes the
`summary` field because the field contains the query term `varieties`.

### Wildcard Example

The following query searches for the term `varieties` in fields that begin
with `des` in the `fruit` collection, with the `highlight` option enabled for
fields that begin with `des`.

The $project pipeline stage adds a new field called `highlights`, which
contains highlighting information.

    
    
    db.fruit.aggregate([  
      
       {  
         $search: {  
           "text": {  
             "path": {"wildcard": "des*"},  
             "query": ["variety"]  
           },  
           "highlight": {  
             "path": {"wildcard": "des*"}  
           }  
         }  
       },  
       {  
         $project: {  
           "description": 1,  
           "_id": 0,  
           "highlights": { "$meta": "searchHighlights" }  
         }  
       }  
    ])  
  
The query returns the following results. The fields that begin with `des` are
highlighted.

    
    
     {  
      
       "description" : "Bosc and Bartlett are the most common varieties of pears.",  
       "highlights" : [  
         {  
           "path" : "description",  
           "texts" : [  
             {  
               "value" : "Bosc and Bartlett are the most common ",  
               "type" : "text"  
             },  
             {  
               "value" : "varieties",  
               "type" : "hit"  
             },  
             {  
               "value" : " of pears.",  
               "type" : "text"  
             }  
           ],  
           "score" : 1.2691514492034912 }  
       ]  
     }  
     {  
       "description" : "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp. The most popular varieties are McIntosh, Gala, and Granny Smith.",  
       "highlights" : [  
         {  
           "path" : "description",  
           "texts" : [  
             {  
               "value" : "Apples come in several ",  
               "type" : "text"  
             },  
             {  
               "value" : "varieties",  
               "type" : "hit"  
             },  
             {  
               "value" : ", including Fuji, Granny Smith, and Honeycrisp. ",  
               "type" : "text"  
             }  
           ],  
           "score" : 1.0330637693405151  
         },  
         {  
           "path" : "description",  
           "texts" : [  
             {  
               "value" : "The most popular ",  
               "type" : "text"  
             },  
             {  
               "value" : "varieties",  
               "type" : "hit"  
             },  
             {  
               "value" : " are McIntosh, Gala, and Granny Smith.",  
               "type" : "text"  
             }  
           ],  
           "score" : 1.0940992832183838  
         }  
       ]  
     }  
  
### Autocomplete Example

For this example, the `fruit` collection also has the following index
definition.

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "description": [  
           {  
            "type": "autocomplete",  
            "tokenization": "edgeGram",  
            "minGrams": 2,  
            "maxGrams": 15,  
            "foldDiacritics": true  
           }  
          ]  
        }  
      }  
    }  
  
The following query searches for the characters `var` in the `description`
field of the `fruit` collection, with the `highlight` option enabled for the
`description` field.

The $project pipeline stage adds a new field called `highlights`, which
contains highlighting information.

## Important

To highlight the autocomplete indexed version of a path, the autocomplete
operator must be the only operator that uses that path in the query.

    
    
    db.fruit.aggregate([  
      
       {  
         $search: {  
           "autocomplete": {  
             "path": "description",  
             "query": ["var"]  
           },  
           "highlight": {  
             "path": "description"  
           }  
         }  
       },  
       {  
         $project: {  
           "description": 1,  
           "_id": 0,  
           "highlights": { "$meta": "searchHighlights" }  
         }  
       }  
    ])  
  
The query returns the following results.

    
    
    {  
      
     "description": "Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp. The most popular varieties are McIntosh, Gala, and Granny Smith.",  
     "highlights": [  
       {  
         "score": 0.774385392665863,  
         "path": "description",  
         "texts": [  
           { "value": "Apples come in several ", "type": "text" },  
           { "value": "varieties, including Fuji", "type": "hit" },  
           { "value": ", Granny Smith, and Honeycrisp. ", "type": "text" }  
         ]  
       },  
       {  
         "score": 0.7879307270050049,  
         "path": "description",  
         "texts": [  
           { "value": "The most popular ", "type": "text" },  
           { "value": "varieties are McIntosh", "type": "hit" },  
           { "value": ", Gala, and Granny Smith.", "type": "text" }  
         ]  
       }  
     ]  
    },  
    {  
     "description": "Bosc and Bartlett are the most common varieties of pears.",  
     "highlights": [  
       {  
         "score": 0.9964432120323181,  
         "path": "description",  
         "texts": [  
           {  
             "value": "Bosc and Bartlett are the most common ",  
             "type": "text"  
           },  
           { "value": "varieties of pears", "type": "hit" },  
           { "value": ".", "type": "text" }  
         ]  
       }  
     ]  
    }  
  
Atlas Search returns a match on the documents with `_id: 1` and `id_: 2` for
the query string `var` because the `description` field in the `fruit`
collection contains the characters `var` at the beginning of a word. Atlas
Search matches a highlight `hit` more coarsely to your query terms when a
highlighted path is referenced only in the autocomplete operators of the
highlighted query.

### Compound Example

The following query searches for the term `organic` in the `category` field
and `variety` in the `description` field. The `highlight` option in the
`$search` compound query requests highlighting information only for the text
query against the `description` field. Note that the `highlight` option inside
the `$search` stage must be a child of the `$search` stage, and not of any
operator inside the `$search` stage.

The $project pipeline stage adds a new field called `highlights`, which
contains highlighting information.

    
    
    db.fruit.aggregate([  
      
      {  
        "$search": {  
          "compound": {  
            "should": [{  
              "text": {  
                "path": "category",  
                "query": "organic"  
              }  
            },  
            {  
              "text": {  
                "path": "description",  
                "query": "variety"  
              }  
            }]  
          },  
          "highlight": {  
            "path": "description"  
          }  
        }  
      },  
      {  
        "$project": {  
          "description": 1,  
          "category": 1,  
          "_id": 0,  
          "highlights": { "$meta": "searchHighlights" }  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        description: 'Apples come in several varieties, including Fuji, Granny Smith, and Honeycrisp. The most popular varieties are McIntosh, Gala, and Granny Smith.',  
        category: 'organic',  
        highlights: [  
          {  
            score: 1.0330637693405151,  
            path: 'description',  
            texts: [  
              { value: 'Apples come in several ', type: 'text' },  
              { value: 'varieties', type: 'hit' },  
              {  
                value: ', including Fuji, Granny Smith, and Honeycrisp. ',  
                type: 'text'  
              }  
            ]  
          },  
          {  
            score: 1.0940992832183838,  
            path: 'description',  
            texts: [  
              { value: 'The most popular ', type: 'text' },  
              { value: 'varieties', type: 'hit' },  
              {  
                value: ' are McIntosh, Gala, and Granny Smith.',  
                type: 'text'  
              }  
            ]  
          }  
        ]  
      },  
      {  
        description: 'Bosc and Bartlett are the most common varieties of pears.',  
        category: 'nonorganic',  
        highlights: [  
          {  
            score: 1.2691514492034912,  
            path: 'description',  
            texts: [  
              {  
                value: 'Bosc and Bartlett are the most common ',  
                type: 'text'  
              },  
              { value: 'varieties', type: 'hit' },  
              { value: ' of pears.', type: 'text' }  
            ]  
          }  
        ]  
      }  
    ]

