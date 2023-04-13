Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Construct a Query Path

Share Feedback

On this page

  * Overview
  * Usage
  * Examples
  * Single Field Search
  * Multiple Field Search
  * Alternate Analyzer Search
  * Nested Field Search
  * Wildcard Field Search

## Overview

The `path` parameter is used by the Atlas Search operators to specify the
field or fields to be searched. It may contain:

  * A string

  * An array of strings

  * A multi analyzer specification

  * An array containing a combination of strings and multi analyzer specifications

## Note

Not all operators can use all the different types of paths. See the
documentation for each individual operator for details on what types of path
it supports.

## Usage

 **To search only a single indexed field** , use a quoted string in the `path`
parameter. The following example searches a field named `description`.

    
    
    "path": "description"  
      
  
 **To search multiple indexed fields** , use an array of quoted strings in the
`path` parameter. Documents which match on any of the specified fields are
included in the result set. The following example searches the `description`
and `type` fields.

    
    
    "path": [ "description", "type" ]  
      
  
## Note

The `multi` path option is available only to fields of type string.

If your index definition contains a field with multiple analyzers, you can
specify which one to use. The `path` parameter can take an object with the
following fields:

Field

|

Description  
  
|  
  
`value`

|

The name of the field to search.  
  
`multi`

|

The name of the alternate analyzer specified in a `multi` object in an index
definition. To learn more, see Multi Analyzer.  
  
`wildcard`

|

The object containing the wildcard character `*` to match any character in the
name of the field to search, including nested fields. A wildcard path:

  * Must be defined as an object.

  * Cannot contain the `value` or `multi` option.

  * Cannot contain multiple consecutive wildcard characters such as `**`.

Wildcard path is only accepted by the following operators:

  * phrase

  * regex

  * text

  * wildcard

Wildcard path is also accepted for highlighting.  
  
In the following index definition, fields named `names` and `notes` use the
standard analyzer. A field named `comments` uses `standard` as its default
analyzer, and it also specifies a `multi` named `mySecondaryAnalyzer` which
uses the lucene.whitespace analyzer.

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "names": {  
            "type": "string",  
            "analyzer": "lucene.standard"  
          },  
          "notes": {  
            "type": "string",  
            "analyzer": "lucene.standard"  
          },  
          "comments": {  
            "type": "string",  
            "analyzer": "lucene.standard",  
            "multi": {  
              "mySecondaryAnalyzer": {  
                "analyzer": "lucene.whitespace",  
                "type": "string"  
              }  
            }  
          }  
        }  
      }  
    }  
  
The following `path` example searches the `comments` field using the `multi`
named `mySecondaryAnalyzer` in the index definition.

    
    
    "path": { "value": "comments", "multi": "mySecondaryAnalyzer" }  
      
  
 **To search a combination of indexed fields and fields with multiple
analyzers** , use an array. The following example searches the `names` and
`notes` fields with the default analyzer, and the `comments` field using the
`multi` named `mySecondaryAnalyzer` in the index definition.

    
    
    "path": [ "names", "notes", { "value": "comments", "multi": "mySecondaryAnalyzer" } ]  
      
  
The following `path` example searches all the fields that contain the letter
`n` followed by any characters, and the `comments` field using the `multi`
named `mySecondaryAnalyzer` in the index definition.

    
    
    "path": [{ "wildcard": "n*" }, { "value": "comments", "multi": "mySecondaryAnalyzer" }]  
      
  
## Examples

The following examples use a collection named `cars` which has the following
documents:

    
    
    {  
      
      "_id" : 1,  
      "type" : "sedan",  
      "make" : "Toyota",  
      "description" : "Blue four-door sedan, lots of trunk space. Three  
      to four passengers."  
    }  
    {  
      "_id" : 2,  
      "type" : "coupe",  
      "make" : "BMW",  
      "description" : "Red two-door convertible, driver's-side airbag."  
    }  
    {  
      "_id" : 3,  
      "type" : "SUV",  
      "make" : "Ford",  
      "description" : "Black four-door SUV, three rows of seats."  
    }  
  
Static field mappings allow you to specify how individual fields within a
collection should be indexed and searched.

The index definition for the `cars` collection is as follows:

    
    
    {  
      
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "make": {  
            "type": "string",  
            "analyzer": "lucene.standard"  
          },  
          "description": {  
            "type": "string",  
            "analyzer": "lucene.standard",  
            "multi": {  
              "simpleAnalyzer": {  
                "analyzer": "lucene.simple",  
                "type": "string"  
              }  
            }  
          }  
        }  
      }  
    }  
  
The preceding index definition specifies that the `make` field is indexed with
the standard analyzer. The `description` field uses the `standard` analyzer by
default, but it can also use the simple analyzer by specifying
`simpleAnalyzer` with the `multi` parameter.

### Single Field Search

The following example searches for the string `Ford` in the `make` field:

    
    
    db.cars.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "Ford",  
            "path": "make"  
          }  
        }  
      }  
    ])  
  
The preceding example returns the document with `_id: 3`.

### Multiple Field Search

The following example uses an array of fields in the `path` parameter to
search for the string `blue` in either the `make` or the `description` field.

    
    
    db.cars.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "blue",  
            "path": [ "make", "description" ]  
          }  
        }  
      }  
    ])  
  
The preceding query returns the following result:

    
    
    {  
      
      "_id" : 1,  
      "type" : "sedan",  
      "make" : "Toyota",  
      "description" : "Blue four-door sedan, lots of trunk space. Three to four  
      passengers."  
    }  
  
### Alternate Analyzer Search

#### Simple Analyzer Example

The following example uses the `multi` named `simpleAnalyzer` in the index
definition, which uses the simple analyzer.

The query searches the `description` field for the string `driver`.

    
    
    db.cars.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "driver",  
            "path": { "value": "description", "multi": "simpleAnalyzer" }  
          }  
        }  
      }  
    ])  
  
The preceding query returns the following result:

    
    
    {  
      
      "_id" : 2,  
      "type" : "coupe",  
      "make" : "BMW",  
      "description" : "Red two-door convertible, driver's-side airbag."  
    }  
  
The simple analyzer indexes `driver's side airbag` as `[driver s side
airbag`], so it matches on `driver`.

By contrast, the default standard analyzer indexes `driver's side airbag` as
`[driver's side airbag`], so it would match on `driver's` or `side` but not
`driver`.

#### Whitespace Analyzer Example

Suppose the `multi` object in the index definition for the `cars` collection
is the following:

    
    
    "multi": {  
      
      "simpleAnalyzer": {  
        "analyzer": "lucene.whitespace",  
        "type": "string"  
      }  
    }  
  
The following example uses the `multi` named `simpleAnalyzer` in the index
definition, which uses the whitespace analyzer.

    
    
    db.cars.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "Three",  
            "path": { "value": "description", "multi": "simpleAnalyzer" }  
          }  
        }  
      }  
    ])  
  
The preceding query returns the following result:

    
    
    {  
      
      "_id" : 1,  
      "type" : "sedan",  
      "make" : "Toyota",  
      "description" : "Blue four-door sedan, lots of trunk space. Three to  
      four passengers."  
    }  
  
For the above query on the term `Three`, Atlas Search only returns documents
matching the term `Three` and not `three` becuase the whitespace analyzer is
case-sensitive. By contrast, the default standard analyzer is not case-
sensitive and returns all documents matching the term in the query in the
order that they are listed in the collection.

Now, consider the following query:

    
    
    db.cars.aggregate([  
      
      {  
        $search: {  
          "compound": {  
            "should": [  
              {  
                "text": {  
                  "path": "description",  
                  "query": "Three"  
                }  
              },  
              {  
                "text": {  
                  "query": "Three",  
                  "path": { "value" : "description", "multi" : "simpleAnalyzer" },  
                  score: { boost: { value: 2 }}  
                }  
              }  
            ]  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 0,  
          "type": 1,  
          "description": 1,  
          "score": { "$meta": "searchScore" }  
        }  
      }  
    ])  
  
The preceding query returns the following results:

    
    
    {  
      
      "type" : "sedan",  
      "description" : "Blue four-door sedan, lots of trunk space. Three to four passengers seats.",  
      "score" : 1.1092689037322998  
    }  
    {  
      "type" : "SUV",  
      "description" : "Black four-door SUV, three rows of seats.",  
      "score" : 0.17812025547027588  
    }  
  
For the above query, Atlas Search returns documents with both `Three` and
`three`. However, the score of the result with `Three` is higher because while
the document with `three` was matched using the default standard analyzer, the
document with `Three` was matched by both the specified `simpleAnalyzer` and
the default standard analyzer.

The following example uses a collection called `posts` with the following
documents:

    
    
     {  
      
      "_id": 1,  
      "username": "pinto",  
      "post": {  
        "date": "12-03-2018",  
        "forum": "Tofu Recipes",  
        "body": "Spicy Garlic Tofu cooks up crispy in 10 minutes or less.  
                 Serve with broccoli and rice for a delicious vegetarian meal."  
      }  
    }  
    {  
      "_id": 2,  
      "username": "paloma",  
      "post": {  
        "date": "12-08-2018",  
        "forum": "Tofu Recipes",  
        "body": "Crispy Tofu in Shiitake Broth has flavors of citrus and  
                 umami. Great as an appetizer or entree."  
      }  
    }  
  
Dynamic field mappings allow you to index all fields in a collection as
needed.

The index definition for the `posts` collection is as follows:

    
    
    {  
      
      "mappings": {  
        "dynamic": true  
      }  
    }  
  
### Nested Field Search

The following compound query searches the field `post.body` for the string
`broccoli`, and also specifies that the field must not contain the string
`cauliflower`.

    
    
    db.posts.aggregate([  
      
      {  
        $search: {  
          "compound": {  
            "must": {  
              "text": {  
                "query": "broccoli",  
                "path": "post.body"  
              }  
            },  
            "mustNot": {  
              "text": {  
                "query": "cauliflower",  
                "path": "post.body"  
              }  
            }  
          }  
        }  
      }  
    ])  
  
The preceding query returns the document with `_id: 1`, in which the
`posts.body` field contains the string `broccoli`.

### Wildcard Field Search

The following example uses a collection named `cars`, which has the following
documents:

    
    
    {  
      
      "_id" : 1,  
      "type" : "sedan",  
      "make" : "Toyota",  
      "description" : "Four-door sedan, lots of trunk space. Three to four passengers.",  
      "warehouse" : [  
        {  
          "inventory" : 3,  
          "color" : "red"  
        }  
      ]  
    }  
    {  
      "_id" : 2,  
      "type" : "coupe",  
      "make" : "BMW",  
      "description" : "Two-door convertible, driver's-side airbag.",  
      "warehouse" : [  
        {  
          "inventory" : 5,  
          "color" : "black"  
        }  
      ]  
    }  
    {  
      "_id" : 3,  
      "type" : "SUV",  
      "make" : "Ford",  
      "description" : "Four-door SUV, three rows of seats.",  
      "warehouse" : [  
        {  
          "inventory" : 7,  
          "color" : "white"  
        },  
        {  
          "inventory" : 3,  
          "color" : "red"  
        }  
      ]  
    }  
  
The index definition for the `cars` collection is as follows:

    
    
    {  
      
      "mappings": {  
        "dynamic": true  
      }  
    }  
  
The following queries search the fields specified using the wildcard character
`*` for the string `red`.

#### All Fields Search Example

The following query searches _all fields_ for the string `red`.

    
    
    db.cars.aggregate([  
      
      {  
        "$search": {  
          "phrase": {  
            "path": { "wildcard": "*" },  
            "query": "red"  
          }  
        }  
      }  
    ])  
  
The query returns the following results:

    
    
    {  
      
      "_id" : 1,  
      "type" : "sedan",  
      "make" : "Toyota",  
      "description" : "Four-door sedan, lots of trunk space. Three to four passengers.",  
      "warehouse" : [  
        { "inventory" : 3, "color" : "red" }  
      ]  
    }  
    {  
      "_id" : 3,  
      "type" : "SUV",  
      "make" : "Ford",  
      "description" : "Four-door SUV, three rows of seats.",  
      "warehouse" : [  
        { "inventory" : 7, "color" : "white" },  
        { "inventory" : 3, "color" : "red" }  
      ]  
    }  
  
#### Nested Field Search Example

The following query searches the fields nested within the `warehouse` field
for the string `red`.

    
    
    db.cars.aggregate([  
      
      {  
        "$search": {  
          "text": {  
            "path": { "wildcard": "warehouse.*" },  
            "query": "red"  
          }  
        }  
      }  
    ])  
  
The query returns the following results:

    
    
    {  
      
      "_id" : 1,  
      "type" : "sedan",  
      "make" : "Toyota",  
      "description" : "Four-door sedan, lots of trunk space. Three to four passengers.",  
      "warehouse" : [  
        { "inventory" : 3, "color" : "red" }  
      ]  
    }  
    {  
      "_id" : 3,  
      "type" : "SUV",  
      "make" : "Ford",  
      "description" : "Four-door SUV, three rows of seats.",  
      "warehouse" : [  
        { "inventory" : 7, "color" : "white" },  
        { "inventory" : 3, "color" : "red" }  
      ]  
    }  
  
← wildcardCustomize and Normalize the Score in Results →

