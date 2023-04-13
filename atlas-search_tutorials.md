Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Search Tutorials

Share Feedback

On this page

  * Prerequisites
  * About the Tutorials

The following tutorials take you through the steps of setting up and querying
an Atlas Search index.

## Prerequisites

To complete these tutorials, you must have the following:

  * An Atlas cluster with MongoDB version 4.2 or higher.

  * The sample data loaded into your Atlas cluster.

  * One of the following applications to run queries on your Atlas cluster:

    * `mongosh`

    * Compass

    * C#

    * Go

    * Java

    * MongoDB Node Driver

    * Pymongo

## About the Tutorials

  * The How to Use Autocomplete with Atlas Search tutorial describes how to create and query an Atlas Search index configured with an `autocomplete` field using the `autocomplete` operator. We will create the Atlas Search index on the `sample_mflix.movies` collection and index `title` field text values for autocompletion. We will run Atlas Search queries using the `autocomplete` operator to search the indexed field for a sequence of characters.

  * The How to Run Atlas Search Compound Queries with Weighted Fields tutorial describes how to create a dynamic index and run compound queries with custom scoring. The queries search the `sample_mflix.movies` collection and alter the relevance score of the documents in the result using `constant`, `boost`, and `function` options.

  * The How to Run Atlas Search Queries with a Date Range Filter tutorial describes how to create a dynamic index and run compound queries that use the `range` operator. The queries search the `sample_mflix.movies` collection for movies between a specified date range.

  * The How to Run Atlas Search Queries Against Objects in Arrays tutorial demonstrates how to index fields of type string inside an array of objects and run Atlas Search queries against the indexed fields.

  * The How to Run an Atlas Search Compound Geo JSON Query tutorial describes how to create an index on the `sample_airbnb.listingsAndReviews` collection and run a query that returns documents with the `name`, `address`, and `property_type` of each property within a specified polygon defined using `coordinates`. Atlas Search results reflect a preference for properties of type `condominium`, and each document in the result is assigned a relevance `score`, returned in order from highest to lowest.

  * The How to Use Facets with Atlas Search tutorial describes how to create an index with a facet definition for the `sample_mflix.movies` collection and run queries against the faceted fields for results grouped by values and ranges in the specified, faceted fields, including a count for each of those groups.

  * The How to Run Partial Match Atlas Search Queries tutorial describes how to create an index on the `sample_mflix.movies` collection and run case-sensitive partial match queries against the indexed field using autocomplete, phrase, regex, and wildcard operators.

  * The How to Use Synonyms with Atlas Search tutorial describes how to add a collection that configures words as synonyms, create an index that defines synonym mappings on the `sample_mflix.movies` collection, and run Atlas Search queries against the `title` field using words that are configured as synonyms.

  * The How to Run Multilingual Atlas Search Queries tutorial describes how to create an index that uses a language analyzer and perform a multilingual search against the `sample_mflix.movies` collection. The queries search the `sample_mflix.movies` collection for full movie plots that contain a multilingual term.

  * The How to Define a Custom Analyzer and Run an Atlas Search Diacritic-Insensitive Query tutorial describes how to create an index that uses a custom analyzer and perform a diacritic-insensitive search against the `sample_mflix.movies` collection. The query searches the `sample_mflix.movies` collection for movie titles that contain the given term regardless if the term contains diacritics.

  * The How to Sort Your Atlas Search Results for Your Perfomance Needs tutorial describes how to index and store fields on `mongot` for interim operations such as sort, run queries against the indexed fields, and then sort the results on the returned fields using `$sort` and `score`.

  * The How to Run Atlas Search String Queries Against Date and Numeric Fields tutorial describes how to run queries against numeric and date fields using operators that support only string queries. The queries search for properties that were listed on certain dates and allow them to stay up to a certain number of days.

  * The How to Run Atlas Search Queries Across Collections contains tutorials that describe how to run queries across multiple collections by first combining collections using `$lookup`, and `$unionWith`, and then running `$search` queries against the collections.

  * The How to Build a Search UI with Atlas App Services describes how to set up Atlas and use Atlas App Services to run queries and build a search UI that uses Searchbox and ReactiveSearch UI libraries.

  * The How to Paginate Query Results describes how to use `$skip` and `$limit` after the `$search` stage to paginate query results, and the `SEARCH_META` Aggregation Variable to return the total documents found.

## Tip

### Want more Atlas Search content?

  * Take Unit 9 of the Intro To MongoDB Course on MongoDB University for an overview of Atlas Search and lessons on creating Atlas Search indexes, running `$search` queries using compound operators, and grouping results using facet.

  * Visit the MongoDB Developer Center for more real-world Atlas Search examples.

  * Try the full-text search examples in the Practical MongoDB Aggregations Book.

← Step 2: Run Atlas Search QueriesHow to Use Autocomplete with Atlas Search →

