Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# regex

Share Feedback

On this page

  * Definition
  * Syntax
  * Options
  * Behavior
  * Lucene Regular Expression Behavior
  * Examples

## Definition

`regex`

    

`regex` interprets the `query` field as a regular expression. `regex` is a
term-level operator, meaning that the `query` field isn't analyzed.

## Tip

### See also:

  * Analyzers.

  * Analyzed field example.

## Note

The regular expression language available to the `regex` operator is a limited
subset of the PCRE library.

For detailed information, see the Class RegExp documentation.

## Syntax

`regex` has the following syntax:

    
    
    1| {  
    |  
    2|   $search: {  
    3|     "index": <index name>, // optional, defaults to "default"  
    4|     "regex": {  
    5|       "query": "<search-string>",  
    6|       "path": "<field-to-search>",  
    7|       "allowAnalyzedField": <boolean>,  
    8|       "score": <options>  
    9|     }  
    10|   }  
    11| }  
  
## Options

`regex` uses the following terms to construct a query:

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

`regex` is a term-level operator, meaning that the `query` field is not
analyzed. Regular expression searches work well with the keyword analyzer,
because it indexes fields one word at a time. To do a case-sensitive search,
do not use the default analyzer, standard analyzer, because the `standard`
analyzer lower cases all terms. Specify a different analyzer instead.

It is possible to use the `regex` operator to perform searches on an analyzed
field by setting the `allowAnalyzedField` option to `true`, but you may get
unexpected results.

## Example

Searching for `*Star Trek*` on a field indexed with the `keyword` analyzer
finds all documents in which the field contains the string `Star Trek` in any
context. Searching for `*Star Trek*` on a field indexed with the standard
analyzer finds nothing, because there is a space between `Star` and `Trek`,
and the index contains no spaces.

## Lucene Regular Expression Behavior

The Atlas Search `regex` operator uses the Lucene regular expression engine,
which differs from Perl Compatible Regular Expressions.

### Reserved characters

The following characters are reserved as operators when used in regular
expressions:

`. ? + * | { } [ ] ( ) " \ @`

To use any of the above characters literally in a matching expression, precede
it with a `\` character.

## Example

`who\?` _matches "who?"_

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
      
  
### Supported Operators

Operator

|

Description

|

Example  
  
||  
  
`.`

|

Matches any character.

|

`x.z` _matches "xyz", "xaz", etc._  
  
`?`

|

The preceding character is optional and matches if it occurs no more than
once.

|

`xyz?` _matches "xy" and "xyz"_  
  
`+`

|

The preceding character matches if it occurs one or more times.

|

`xy+` _matches "xy", "xyy", "xyyy", etc._  
  
`*`

|

The preceding character matches if it occurs any number of times.

|

`xyz*` _matches "xy", "xyz", "xyzz", etc._  
  
`{<number>}`

|

The preceding character matches if it occurs exactly <number> times.

|

`xyz{3}` _matches "xyzzz"_  
  
`|`

|

The `OR` operator. The expression matches if the longer of the two patterns on
either side of the `|` operator matches.

|

`abc|xyz` _matches "abc" or "xyz"_  
  
`()`

|

Characters inside parentheses are treated as a single unit for matching
purposes.

|

`xyz(abc)[2]` _matches "xyzabcabc"_  
  
`[]`

|

Match any of the characters inside the square brackets. Adding a `^` to the
beginning matches any character except those within the square brackets.

|

`[xyz]` _matches "x", "y", and "z"_ `[^abc]` _matches any character except
"a", "b", or "c"_  
  
### Unsupported Operators

`regex` does not support the anchor operators `^` and `$`.

## Examples

The following examples use the `movies` collection in the `sample_mflix`
database with a custom index definition that uses the keyword analyzer. If you
have the sample dataset on your cluster, you can create an Atlas Search index
on the `movies` collection and run the example queries on your cluster.

## Tip

If you've already loaded the sample dataset, follow the Get Started with Atlas
Search tutorial to create an index definition and run Atlas Search queries.

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
  
The following example searches all `title` fields for movie titles that end
with the word `Seattle`. The `(.*)` regular expression matches any number of
characters.

    
    
    1| db.movies.aggregate([  
    |  
    2|    {  
    3|       "$search": {  
    4|          "regex": {  
    5|             "path": "title",  
    6|             "query": "(.*) Seattle"  
    7|          }  
    8|       }  
    9|    },  
    10|    {  
    11|       $project: {  
    12|          "_id": 0,  
    13|          "title": 1  
    14|       }  
    15|    }  
    16| ])  
  
The above query returns the following results:

    
    
    { "title" : "Sleepless in Seattle" }  
      
    { "title" : "Battle in Seattle" }  
  
The following example uses the regular expression `[0-9]{2} (.){4}s` to find
movie titles which begin with a 2-digit number followed by a space, and end
with a 5-letter word ending in `s`.

    
    
    1| db.movies.aggregate([  
    |  
    2|    {  
    3|       "$search": {  
    4|          "regex": {  
    5|             "path": "title",  
    6|             "query": "[0-9]{2} (.){4}s"  
    7|          }  
    8|       }  
    9|    },  
    10|    {  
    11|       $project: {  
    12|          "_id": 0,  
    13|          "title": 1  
    14|       }  
    15|    }  
    16| ])  
  
The above query returns the following results:

    
    
    { "title" : "20 Dates" }  
      
    { "title" : "25 Watts" }  
    { "title" : "21 Grams" }  
    { "title" : "13 Lakes" }  
    { "title" : "18 Meals" }  
    { "title" : "17 Girls" }  
    { "title" : "16 Acres" }  
    { "title" : "26 Years" }  
    { "title" : "99 Homes" }  
    { "title" : "45 Years" }  
  
← rangespan →

