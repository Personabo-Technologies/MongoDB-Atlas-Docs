Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# wildcard

Select your language

MongoDB Shell

On this page

  * Definition
  * Syntax
  * Options
  * Behavior
  * Examples

## Definition

`wildcard`

    

The `wildcard` operator enables queries which use special characters in the
search string that can match any character.

Character

|

Description  
  
|  
  
`?`

|

Matches any single character.  
  
`*`

|

Matches 0 or more characters.  
  
`\`

|

Escape character.  
  
`wildcard` is a term-level operator, meaning that the `query` field is not
analyzed. Term-level operators work well with the Keyword Analyzer, because
the `query` field is treated as a single term, with special characters
included. For an example of querying against an analyzed `query` field vs. a
non-analyzed `query` field, see the analyzed field example.

## Syntax

`wildcard` has the following syntax:

    
    
    {  
      
      $search: {  
        "index": <index name>, // optional, defaults to "default"  
        "wildcard": {  
          "query": "<search-string>",  
          "path": "<field-to-search>",  
          "allowAnalyzedField": <boolean>,  
          "score": <options>  
        }  
      }  
    }  
  
## Options

`wildcard` uses the following terms to construct a query:

Field

|

Type

|

Description

|

Necessity

|

Default  
  
||||  
  
`query`

|

string or array of strings

|

String or strings to search for.

|

yes

|  
  
`path`

|

string or array of strings

|

Indexed field or fields to search. You can also specify a wildcard path to
search. See path construction for more information.

|

yes

|  
  
`allowAnalyzedField`

|

boolean

|

Must be set to `true` if the query is run against an analyzed field.

|

no

|

`false`  
  
`score`

|

object

|

Modify the score assigned to matching search term results. Options are:

  * `boost`: multiply the result score by the given number.

  * `constant`: replace the result score with the given number.

|

no

|  
  
## Behavior

`wildcard` is a term-level operator, meaning that the `query` field is not
analyzed. It is possible to use the `wildcard` operator to perform searches on
a field analyzed during indexing by setting the `allowAnalyzedField` option to
`true`, but results will reflect that the query text is not analyzed.

## Example

Suppose that a field `foo bar baz` is indexed with the standard analyzer.
Atlas Search analyzes and indexes the field as `foo`, `bar` and `baz`.
Searching for `foo bar*` on this field finds nothing, because the wildcard
operator treats `foo bar*` as a single search term with a wildcard at the end.
In other words, Atlas Search searches the field for any term that begins with
`foo bar` but finds nothing, because no term exists.

## Example

Searching for `*Star Trek*` on a field indexed with the `keyword` analyzer
finds all documents in which the field contains the string `Star Trek` in any
context. Searching for `*Star Trek*` on a field indexed with the standard
analyzer finds nothing, because there is a space between `Star` and `Trek`,
and the index contains no spaces.

### Escape Character Behavior

When using the escape character in `mongosh` or with a driver, you must use a
double backslash before the character to be escaped.

## Example

To create a wildcard expression which searches for any string containing a
literal asterisk in an aggregation pipeline, use the following expression:

    
    
    "*\\**"  
      
  
The first and last asterisks act as wildcards which match any characters, and
the `\\*` matches a literal asterisk.

## Note

Use the following expression to escape a literal backslash:

    
    
    "*\\\*"  
      
  
* * *

➤ Use the **Select your language** drop-down menu to set the language of the
examples on this page.

* * *

## Examples

The following examples use the `movies` collection in the `sample_mflix`
database with a custom index definition that uses the keyword analyzer. If you
have the sample dataset on your cluster, you can create an Atlas Search index
on the `movies` collection and run the example queries on your cluster.

## Tip

If you've already loaded the sample dataset, follow the Get Started with Atlas
Search tutorial to create an index definition and run Atlas Search queries.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

Run the following command at `mongosh` prompt to use the `sample_mflix`
database:

    
    
    use sample_mflix  
      
  
MongoDB Shell

### Index Definition

The following index definition indexes the `title` field in the `movies`
collection with the keyword analyzer:

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "fields": {  
    4|       "title": {  
    5|         "analyzer": "lucene.keyword",  
    6|         "type": "string"  
    7|       }  
    8|     }  
    9|   }  
    10| }  
  
The following example searches all `title` fields for movie titles that begin
with `Green D`, followed by any number of other characters.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "wildcard": {  
            "path": "title",  
            "query": "Green D*"  
          }  
        }  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1  
        }  
      }  
    ])  
  
MongoDB Shell

The above query returns the following results:

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    { "title" : "Green Dolphin Street" }  
      
    { "title" : "Green Dragon" }  
  
MongoDB Shell

The following example searches all `title` fields for movie titles that begin
with the string `Wom?n` (where `?` may be any single character), followed by a
space and then any number of additional characters. The `$limit` stage limits
the results to 5 documents, while the `$project` stage limits the results to
only the `title` field.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "wildcard": {  
            "path": "title",  
            "query": "Wom?n *"  
          }  
        }  
      },  
      {  
        "$limit": 5  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1  
        }  
      }  
    ])  
  
MongoDB Shell

The above query returns the following results:

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    { "title" : "Woman of the Year" }  
      
    { "title" : "Woman in a Dressing Gown" }  
    { "title" : "Woman in the Dunes" }  
    { "title" : "Women in Love" }  
    { "title" : "Women on the Verge of a Nervous Breakdown" }  
  
MongoDB Shell

### Escape Character Example

The following example searches for documents in which the `title` field ends
with a question mark.

## Note

The following example is intended to run in `mongosh`. For more information
about using the escape characters with a driver, see Escape Character
Behavior.

The `*` character in the `query` field matches any characters, and the `\\?`
string matches a literal question mark. The `$limit` stage limits the results
to 5 documents, while the `$project` stage limits the results to only the
`title` field.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    db.movies.aggregate([  
      
      {  
        "$search": {  
          "wildcard": {  
            "path": "title",  
            "query": "*\\?"  
          }  
        }  
      },  
      {  
        "$limit": 5  
      },  
      {  
        "$project": {  
          "_id": 0,  
          "title": 1  
        }  
      }  
    ])  
  
MongoDB Shell

The above query returns the following results:

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

    
    
    { "title" : "Where Are My Children?" }  
      
    { "title" : "Who Killed Cock Robin?" }  
    { "title" : "What's Opera, Doc?" }  
    { "title" : "Will Success Spoil Rock Hunter?" }  
    { "title" : "Who Was That Lady?" }  
  
MongoDB Shell

← textConstruct a Query Path →

