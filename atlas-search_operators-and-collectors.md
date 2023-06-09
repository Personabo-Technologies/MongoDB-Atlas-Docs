Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Use Operators and Collectors in Atlas Search Queries

Share Feedback

On this page

  * Operators
  * Collectors

## Operators

The `$search` aggregation pipeline stage has the following operators:

Operator

|

Description  
  
|  
  
autocomplete

|

Performs a search-as-you-type query from an incomplete input string.  
  
compound

|

Combines other operators into a single query.  
  
embeddedDocument

|

Queries fields in embedded documents, which are documents that are elements of
an array.  
  
equals

|

Works in conjunction with the boolean and objectId data types.  
  
exists

|

Tests for the presence of a specified field.  
  
geoShape

|

Queries for values with specified geo shapes.  
  
geoWithin

|

Queries for points within specified geographic shapes.  
  
moreLikeThis

|

Queries for similar documents.  
  
near

|

Queries for values near a specified number, date, or geo point.  
  
phrase

|

Searches documents for terms in an order similar to the query.  
  
queryString

|

Supports querying a combination of indexed fields and values.  
  
range

|

Queries for values within a specific numeric or date range.  
  
regex

|

Interprets the `query` field as a regular expression.  
  
span

|

Specifies relative positional requirements for query predicates within
specified regions of a text field.  
  
text

|

Performs textual analyzed search.  
  
wildcard

|

Supports special characters in the query string that can match any character.  
  
## Collectors

Collectors return a document representing the metadata results, typically an
aggregation over the matching search results.

The Atlas Search aggregation pipeline stage has the following collector:

Operator

|

Description  
  
|  
  
facet

|

Groups query results by values or ranges in specified, faceted fields and
returns the count for each of those groups.  
  
← Choose an Aggregation Pipeline Stageautocomplete →

