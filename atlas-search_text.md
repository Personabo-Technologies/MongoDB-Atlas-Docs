Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# text

Share Feedback

On this page

  * Definition
  * Syntax
  * Fields
  * Examples
  * Basic Example
  * Fuzzy Examples
  * Synonyms Examples

## Definition

The `text` operator performs a full-text search using the analyzer that you
specify in the index configuration. If you omit an analyzer, the `text`
operator uses the default standard analyzer.

## Syntax

`text` has the following syntax:

    
    
    {  
      
      $search: {  
        "index": <index name>, // optional, defaults to "default"  
        "text": {  
          "query": "<search-string>",  
          "path": "<field-to-search>",  
          "fuzzy": <options>,  
          "score": <options>,  
          "synonyms": "<synonyms-mapping-name>"  
        }  
      }  
    }  
  
## Fields

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`query`

|

string or array of strings

|

The string or strings to search for. If there are multiple terms in a string,
Atlas Search also looks for a match for each term in the string separately.

|

Required  
  
`path`

|

string or array of strings

|

The indexed field or fields to search. You can also specify a wildcard path to
search. See path construction for more information.

|

Required  
  
`fuzzy`

|

document

|

Enable fuzzy search. Find strings which are similar to the search term or
terms. You can't use `fuzzy` with `synonyms`.

|

Optional  
  
`fuzzy.maxEdits`

|

integer

|

Maximum number of single-character edits required to match the specified
search term. Value can be `1` or `2`. The default value is `2`. Uses Damerau-
Levenshtein distance.

|

Optional  
  
`fuzzy.prefixLength`

|

integer

|

Number of characters at the beginning of each term in the result that must
exactly match. The default value is `0`.

|

Optional  
  
`fuzzy.maxExpansions`

|

integer

|

The maximum number of variations to generate and search for. This limit
applies on a per-token basis. The default value is `50`.

|

Optional  
  
`score`

|

document

|

The score assigned to matching search term results. Use one of the following
options to modify the score:

  * `boost`: multiply the result score by the given number.

  * `constant`: replace the result score with the given number.

|

Optional  
  
`synonyms`

|

string

|

Required for running queries using synonyms.

Name of the synonym mapping definition in the index definition. Value can't be
an empty string. You can't use `fuzzy` with `synonyms`.

`text` queries that use synonyms look for a conjunction ( _AND_ ) of query
tokens. `text` queries that don't use synonyms search for a disjunction ( _OR_
) of query tokens. To run `text` queries that use synonyms and search for a
disjunction ( _OR_ ) of query tokens also, use the compound operator. For
example:

    
    
    | "compound": {  
      
      "should": [  
        {  
          "text": {  
            "path": "a",  
            "query": "my query",  
            "synonyms": "mySynonyms"  
          }  
        },  
        {  
          "text": {  
            "path": "a",  
            "query": "my query"  
          }  
        }  
      ]  
    }  
  
## Note

The amount of time that Atlas Search takes to execute queries that use synonym
mappings depends on the number and size of documents in the synonym source
collection. A query that uses a synonym mapping that is based on very few
synonym documents might be faster than a query that uses a synonym mapping
that is based on many synonym documents.

Optional  
  
## Examples

The Basic and Fuzzy examples below use the `movies` collection in the
`sample_mflix` database. After loading the sample dataset into your cluster,
create the Atlas Search index on the `title` field and run the example queries
on your cluster.

## Tip

If you've already loaded the sample dataset, follow the Get Started with Atlas
Search tutorial to create an index definition and run Atlas Search queries.

The Synonyms examples below use the `user_feedback.comments` and
`user_feedback.synonyms` collections and the index definition described in
Define Synonym Mappings. After loading the `user_feedback.comments` and
`user_feedback.synonyms` collections and configuring the index definition for
the collection, you can run the queries below.

### Basic Example

The following Atlas Search example uses the `text` operator to search the
`title` field in the `movies` collection for the term `surfer`.

## Example

The following query searches the `title` field for the term `surfer`. It
includes a $project stage to:

  * Exclude all fields except `title`

  * Add a field named `score`

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "path": "title",  
            "query": "surfer"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 0,  
          "title": 1,  
          score: { $meta: "searchScore" }  
        }  
      }  
    ])  
  
The above query returns the following results:

    
    
    { "title" : "Soul Surfer", "score" : 4.572484970092773 }  
      
    { "title" : "Little Surfer Girl", "score" : 3.9323642253875732 }  
    { "title" : "Fantastic 4: Rise of the Silver Surfer", "score" : 2.520784616470337 }  
  
### Fuzzy Examples

The following queries use the `text` operator to search the `title` field in
the `movies` collection for terms that are within one character variation of
each term in the `query` phrase `naw yark`. Atlas Search returns different
results depending on whether you use the default `fuzzy` options or define the
`maxExpansions`, `prefixLength`, or `maxEdits` fields.

Click the following tabs for example queries that use default and specified
options:

Default Example

maxExpansions Example

prefixLength Example

## Example

The following query searches the `title` field for the phrase `naw yark`. It
uses the `fuzzy` default options where:

  * `maxEdits` allows up to two character variation of each term in the given phrase to match the query to a document.

  * `maxExpansions` considers up to fifty similar terms for each term in `naw yark` to find matches.

  * `prefixLength` is disabled.

The query also includes a $limit stage to limit the output to 10 results and a
$project stage to:

  * Exclude all fields except `title`

  * Add a field named `score`

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "path": "title",  
            "query": "naw yark",  
            "fuzzy": {}  
          }  
        }  
      },  
      {  
        $limit: 10  
      },  
      {  
        $project: {  
          "_id": 0,  
          "title": 1,  
          score: { $meta: "searchScore" }  
        }  
      }  
    ])  
  
The above query returns the following results:

    
    
    { "title" : "New York, New York", "score" : 4.392756462097168 }  
      
    { "title" : "New York", "score" : 4.050914287567139 }  
    { "title" : "New York Stories", "score" : 3.4838104248046875 }  
    { "title" : "New York Minute", "score" : 3.4838104248046875 }  
    { "title" : "Synecdoche, New York", "score" : 3.4838104248046875 }  
    { "title" : "New York Doll", "score" : 3.4838104248046875 }  
    { "title" : "Little New York", "score" : 3.4838104248046875 }  
    { "title" : "Escape from New York", "score" : 3.0559897422790527 }  
    { "title" : "King of New York", "score" : 3.0559897422790527 }  
    { "title" : "Naked in New York", "score" : 3.0559897422790527 }  
  
### Synonyms Examples

The following examples use the `text` operator to search the `comments` field
in the `user_feedback.comments` collection. Atlas Search returns results based
on the type of mapping in the synonym source collection,
`user_feedback.synonyms`, specified in the synonym mapping definition of the
index for the `user_feedback.comments` collection.

## Note

To learn more about the `user_feedback.comments` and `user_feedback.synonyms`
collections and the index definition for the `user_feedback.comments`
collection, see Example in the Define Synonym Mappings in Your Atlas Search
Index page.

#### `equivalent` Mapping Example

The following query searches the `comments` field for the word `dress`. It
uses the synonym mapping named `mySynonyms` in the index for the collection to
also search for words that are configured to be synonyms of the word `dress`.

    
    
    db.comments.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "path": "comments",  
            "query": "dress",  
            "synonyms": "mySynonyms"  
          }  
        }  
      }  
    ])  
  
The preceding query returns the following results:

    
    
    {  
      
      "_id" : ObjectId("60e5f7d65f32d78cb3a3cc7a"),  
      "type" : "apparel store",  
      "comments" : "Beautiful apparel for the bride."  
    }  
  
Atlas Search returns the above document because `dress` is configured to be
synonym of `apparel` and `attire` using `equivalent` mappings in the synonym
source collection, `user_feedback.synonyms`. Atlas Search returns the above
document for searches on `apparel` and `attire` also because all three words
are configured to be synonyms of one another in the synonym source collection.

#### `explicit` Mapping Example

The following query searches the `comments` field for the word `boat`. It uses
the synonym mapping named `mySynonyms` in the index for the collection to also
search for words that are configured to be synonyms of the word `boat`.

    
    
    db.comments.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "path": "comments",  
            "query": "boat",  
            "synonyms": "mySynonyms"  
          }  
        }  
      }  
    ])  
  
The preceding query returns the following results:

    
    
    {  
      
      "_id" : ObjectId("60e5f7e25f32d78cb3a3cdc4"),  
      "type" : "recreation rental",  
      "comments" : "Sails as well as the day it was made."  
    }  
  
Atlas Search returns the above document because `boat` is configured to
consider words `boat`, `vessel`, and `sail` as synonyms using `explicit`
mappings in the synonym source collection, `user_feedback.synonyms`. However,
Atlas Search doesn't return any results for a query on `vessel` or `sail`
because neither word is configured to consider any of the other words as
synonyms.

← spanwildcard →

