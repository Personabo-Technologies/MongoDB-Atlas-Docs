Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Search Best Practices

Share Feedback

Use the following recommended best practices to determine whether to refactor
your applications that use MongoDB `$text` and `$regex` or migrate your
applications to Atlas Search `$search`. The following table shows how MongoDB
`$regex`, `$text`, and Atlas Search `$search` address your application's
requirements.

If your application requires...

|

Use...

|

Because...  
  
||  
  
Datastore to respect write concerns

|

`$regex`

|

For transactions with heavy reads after writes, we recommend `$regex`. For
`$search`, reads after writes should be rare.  
  
Cluster optimized for write performance

|

`$search`

|

Atlas Search indexes don't degrade cluster write performance.  
  
Searching through large data sets

|

`$search`

|

Atlas Search uses an inverted index, which enables fast document retrieval at
very large scales.  
  
Language awareness

|

`$search`

|

Atlas Search supports many language analyzers that can tokenize (create
searchable terms) languages, remove stopwords, and interpret diacritics for
improved search relevance. To learn more, see How to Run Multilingual Atlas
Search Queries.  
  
Case-insensitive text search

|

`$search`

|

`$search` offers more capabilities than `$regex`.  
  
Highlighting result text

|

`$search`

|

Atlas Search highlighting allows you to contextualize the documents in the
results, which is essential for natural language queries.  
  
Geospatial-aware search queries

|

`$regex` or `$search`

|

MongoDB `$regex` and Atlas Search `$search` treat geospatial parameters
differently. In MongoDB, lines between coordinates are spherical, which is
well-suited for coordinates for long distance such as air flight. Atlas Search
uses Lucene, which draws a straight line between coordinates and is well-
suited for short distance. To learn more, see How to Run an Atlas Search
Compound Geo JSON Query.  
  
On-premises or local deployment

|

`$regex` or `$text`

|

Atlas Search is unavailable for on-premise or local deployment. Atlas Search
is only available for data on the Atlas cluster.  
  
Autocompletion of search queries

|

`$search`

|

For autocomplete of characters (nGrams), Atlas Search includes `edgeGrams` for
left-to-right autocomplete, `nGrams` for autocomplete of languages that don't
have whitespace, and `rightEdgeGram` for autocomplete of languages that you
write and read right-to-left.

For autocomplete of words (wordGrams), Atlas Search includes shingle token
filter, which supports word-based autocomplete by concatenating adjacent words
to create a single token.

To learn more, see How to Use Autocomplete with Atlas Search.  
  
Fuzzy matching on text input

|

`$search`

|

Atlas Search text and autocomplete operators support `fuzzy` matching to
filter on input text and address misspelled words (typos).  
  
Filtering based on multiple strings

|

`$search`

|

Atlas Search compound supports filtering based on more than 10 strings.  
  
Relevance score sorted search

|

`$search`

|

Atlas Search uses the BM25 algorithm for determining the search relevance
score of documents. It supports advanced configuration through `boost`
expressions like multiply and gaussian decay, as well as analyzers, search
operators, and synonyms. To learn more, see How to Run Atlas Search Compound
Queries with Weighted Fields.  
  
Partial indexes

|

`$regex`

|

Atlas Search doesn't support partial indexing.  
  
Patial match

|

`$search`

|

Atlas Search wildcard and autocomplete operators support partial match
queries. To learn more, see How to Run Partial Match Atlas Search Queries.  
  
Single compound index on arrays

|

`$search`

|

Atlas Search term indexes are intersected in a single Atlas Search index and
eliminate the need for compound indexes for filtering on arrays.  
  
Synonyms search

|

`$search`

|

Atlas Search supports synonyms defined in a separate collection, which you can
reference in your search index for use. To learn more, see How to Use Synonyms
with Atlas Search.  
  
Faceting for counts

|

`$search`

|

Atlas Search provides fast counts of documents based on text criteria, and
also supports faceted search for numbers and dates. To learn more, see How to
Use Facets with Atlas Search.  
  
Custom analyzers

|

`$search`

|

Atlas Search supports custom analyzers to suit your specific indexing
requirements. For example, you can index and search email addresses and HTTP
or HTTPS URLs using custom analyzers. To learn more, see How to Define a
Custom Analyzer and Run an Atlas Search Diacritic-Insensitive Query.  
  
Searching phrases or multiple words

|

`$search`

|

Atlas Search phrase operator supports searching for a sequence of terms.  
  
← Atlas Search OverviewUpdate $text Queries with Atlas Search for Improved
Search Performance →

