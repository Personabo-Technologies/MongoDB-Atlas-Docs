Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Search Changelog

Share Feedback

On this page

  * 2023 Releases
  * 2022 Releases
  * 2021 Releases
  * 2020 Releases

## Note

Atlas Search release notes from prior to April 2020 can be found in the Atlas
Changelog.

2023 Releases

## 2023 Releases

### 01 March 2023 Release

  * Introduces the ability to edit your Atlas Search query in the Search Tester.

### 31 January 2023 Release

  * Adds the following language analyzers:

    * `lucene.polish`

    * `lucene.portuguese`

    * `lucene.smartcn`

    * `lucene.sorani`

    * `lucene.thai`

    * `lucene.turkish`

  * Adds the following token filters:

    * englishPossessive

    * flattenGraph

    * kStemming

    * porterStemming

    * spanishPluralStemming

    * stempel

    * wordDelimiterGraph

  * Supports the number data type using the equals operator.

  * Supports synonyms for sharded clusters.

### 25 January 2023 Release

  * Supports the embeddedDocuments type in the Atlas Search visual editor configuration mode in the Atlas UI.

## 2022 Releases

### 02 November 2022 Release

  * Supports statically indexing arrays of strings as How to Index Fields for Autocompletion type and querying the indexed field using the autocomplete operator.

  * Supports dynamically and statically indexing How to Index Numeric Valuess in arrays and querying the indexed How to Index Numeric Valuess in arrays using the range operator only.

  * Supports dynamically and statically indexing How to Index Date Fieldss in arrays and querying the indexed How to Index Date Fieldss in arrays using the range operator only.

  * Supports dynamically and statically indexing How to Index ObjectId Values in Fieldss and arrays of How to Index ObjectId Values in Fieldss and querying the indexed How to Index ObjectId Values in Fieldss using the equals operator.

  * Supports dynamically and statically indexing How to Index Boolean Valuess and arrays of How to Index Boolean Valuess and querying the How to Index Boolean Valuess using the equals operator.

### 03 October 2022 Release

  * Improves performance for storedSource.

### 02 August 2022 Release

  * Upgrades to Atlas Search, which include the following:

    * Querying improvements

      * Supports `\w`, `\W`, `\D`, `\s`, and `\S` regular expressions in the regex query. However, Atlas Search doesn't return results for characters other than `s`, `S`, `w`, `W`, `d`, and `D` in the regex query. We recommend using backslashes according to regex standards.

      * Updates to email tokenizer top-level domains from the IANA Root Zone Database.

    * Highlighting improvements

      * Passage selector truncates long snippets to show a shorter snippet, which fixes the cause for queries failing when the passage is long.

    * Explain output for some queries might look different. If you use explain, verify that the changes don't break logic in your environment.

In addition to the preceding list of changes, you might notice some indexing
and querying performance changes.

  * Introduces moreLikeThis operator to retrieve documents similar to one or more input documents.

### 07 June 2022 Release

  * Supports the facet collector on sharded clusters running MongoDB 6.0 and later.

  * Supports `$search` and `$searchMeta` stages inside `$lookup` and `$unionWith` sub-pipeline.

### 01 June 2022 Release

  * Introduces embedded documents for $elemMatch-like searches.

## Note

The Atlas Search embeddedDocuments index option, embeddedDocument operator,
and `embedded` scoring option are in preview. When an Atlas Search index on a
replica set or single MongoDB shard reaches Lucene's two billion document
limit, Atlas Search doesn't index new documents or apply updates to existing
documents for that index. A solution to accommodate this limitation will be in
place when this feature is generally available. To troubleshoot any issues
related to using this feature, contact Support.

### 27 April 2022 Release

  * Improves performance of stored source fields for faster post-aggregation stages.

  * Improves precision of replication lag metrics reporting.

### 19 April 2022 Release

  * Optimizes internal batching to improve stored source query performance when your query matches a large number of documents (5,000 or more).

### 31 March 2022 Release

  * Introduces an option in the index definition for storing fields on Atlas Search and `$search` option for returning stored fields.

### 09 March 2022 Release

  * Introduces a new `Project Search Index Editor` role to create, view, edit, and delete Atlas Search indexes using the Atlas UI or API.

  * Serves queries using your last valid index if new index definition is invalid.

  * Removes Lucene's default clause limit of `1024` for `BooleanQuery` on dedicated clusters.

## Note

We are extending support for faceting on numeric and date fields using How to
Index Numeric Values and How to Index Date Fields type from August to
September 2022. You must migrate to the How to Index Numeric Values for
Faceted Search and How to Index Date Fields For Faceted Search types in all
index definitions for faceting on numeric and date fields, respectively.

### 01 March 2022 Release

  * Adds How to Index Numeric Values for Faceted Search and How to Index Date Fields For Faceted Search data types for running facet queries on number and date fields respectively.

## Note

We are extending support for faceting on numeric and date fields using How to
Index Numeric Values and How to Index Date Fields type from August to
September 2022. You must migrate to the How to Index Numeric Values for
Faceted Search and How to Index Date Fields For Faceted Search types in all
index definitions for faceting on numeric and date fields, respectively.

### 26 January 2022 Release

  * Adds reverse token filter, which reverses each string token.

## 2021 Releases

### 10 December 2021 Release

  * Adds support for Gaussian decay expressions, which decay, or reduce, document scores by multiplying at a specified rate.

### 03 November 2021 Release

  * Adds asciiFolding token filter for converting alphabetic, numeric, and symbolic unicode characters that are not in the Basic Latin Unicode block to their ASCII equivalents.

### 28 September 2021 Release

Autocomplete improvements in this release:

  * Adds support for analyzers in the index definition for How to Index Fields for Autocompletion.

  * Boosts exact matches in autocomplete operator.

  * Adds `rightEdgeGram` tokenization strategy to create `edgeGram`-like tokens starting at the right side of words (instead of the left side).

Bug fixes in this release:

  * Fixes `objectId` highlighting error.

### 07 Septermber 2021 Release

  * Allows indexes to enter a recovering state and remain available after encountering certain replication errors.

### 13 July 2021 Release

  * Adds support for synonyms, which can be defined in a source collection and mapped to search indexes via the Atlas API.

### 01 June 2021 Release

  * Supports wildcard path for highlight.

### 05 April 2021 Release

  * Adds stopword token filter for removing tokens that match the specified stop words.

### 19 March 2021 Release

  * Adds additional language analyzers, token filters, and tokenizers.

  * Adds support for function scores, which allows you to alter the relevance score of a document using a numeric field in the same document.

### 05 February 2021 Release

  * Supports explain for `$search` queries.

### 16 January 2021 Release

  * Fixes an issue with highlighting raising errors when combined with ObjectID equality operators.

### 14 January 2021 Release

  * Improves performance of initial sync indexing.

## 2020 Releases

### 15 December 2020 Release

  * Adds `maxNumPassages` and `maxCharsToExamine` for highlight.

### 19 November 2020 Release

  * Improves performance of steady state indexing.

### 13 November 2020 Release

  * Fixes a bug in custom analyzers where only the first `charMap` character filter was being executed.

### 1 October 2020 Release

  * Removes downtime requirement when rebuilding modified index definitions.

### 2 September 2020 Release

  * Adds custom analyzers for index definitions and search queries.

### 23 August 2020 Release

  * Adds support for wildcard path.

### 9 June 2020 Release

  * Releases Atlas Search to general availability.

  * Adds support for data types boolean and objectId.

### 18 May 2020 Release

  * Adds a new index option to exclude the `norms` field, allowing a search index to ignore field length when scoring search results.

  * Adds the tokenOrder option to the autocomplete operator, supporting unordered terms in search queries.

  * Improves error messages to facilitate query debugging, including eliminating stack traces and other Java-specific messages.

### 30 April 2020 Release

  * Adds support for geospatial queries, including:

    * A new geo data type for indexing geographic point and shape coordinates.

    * Two new operators, geoWithin and geoShape, to support queries on geospatial data, such as points and polygons.

  * Adds autocomplete features to support better search-as-you-type functionality, including:

    * A new autocomplete operator and index type.

    * Analyzer-agnostic diacritic folding of field values.

    * Scoring options, such as boost and constant.

    * Compound queries that combine autocomplete with other $search operators.

    * n-grams/shingles and edge n-grams from analyzed text.

