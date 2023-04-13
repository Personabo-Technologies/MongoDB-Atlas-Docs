Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Define Synonym Mappings in Your Atlas Search Index

Share Feedback

On this page

  * Syntax
  * Options
  * Synonyms Source Collection Documents
  * Format of Synonyms Source Collection Documents
  * Changes to Synonyms Source Collection Documents
  * `mappingType` Examples
  * `equivalent`
  * `explicit`
  * Example
  * Collection Example
  * Synonym Source Collection Example
  * Index Definition Examples
  * Static Mapping
  * Dynamic Mapping

`synonyms` allow you to index and search your collection for words that have
the same or nearly the same meaning. To configure an Atlas Search index with
synonym mappings, you must:

  1. Create a new collection with properly formatted synonym documents in it. Ensure that:

    * Your collection is in the same database as the index that will reference the collection.

    * You format the documents in the collection as described in the Synonyms Source Collection Documents.

  2. Reference the synonym source collection in a synonym mapping in the index definition.

This page describes the format of the synonyms source collection and how to
define synonym mappings that reference the synonym source collection in your
Atlas Search index. A synonym mapping configures an Atlas Search index to
support queries that apply synonyms from a separate synonym source collection.
You can use the Visual Editor view or the JSON Editor view in the Atlas UI or
the Atlas Search API to create the index. You can use synonyms only in queries
that use the text operator.

## Syntax

`synonyms` has the following syntax in an index definition:

    
    
    1| {   
    |  
    2|   "name": "<index-name>",   
    3|   "analyzer": "<analyzer-for-index>",   
    4|   "searchAnalyzer": "<analyzer-for-query>",   
    5|   "mappings": {   
    6|     "dynamic": <boolean>,   
    7|     "fields": { <field-definition> }   
    8|   },   
    9|   "synonyms": [  
    10|     {  
    11|       "name": "<synonym-mapping-name>",  
    12|       "source": {  
    13|         "collection": "<source-collection-name>"  
    14|       },  
    15|       "analyzer": "<synonym-mapping-analyzer>"  
    16|     }  
    17|   ]   
    18| }  
  
## Options

`synonyms` takes the following fields in an index definition:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`analyzer`

|

string

|

Name of the analyzer to use with this synonym mapping.

## Note

You can use a synonym mapping to query only fields analyzed with the same
analyzer. By default, Atlas Search uses the standard analyzer
(`"lucene.standard"`).

You can use any Atlas Search analyzer except the following:

Language analyzers:

  * `lucene.kuromoji`

  * `lucene.cjk`

Custom analyzer tokenizers and token filters:

  * nGram Tokenizer

  * edgeGram Tokenizer

  * daitchMokotoffSoundex Token Filter

  * nGram Token Filter

  * edgeGram Token Filter

  * shingle Token Filter

  * wordDelimiterGraph Token Filter

## Note

To use synonyms with stop words, you must either index the field using the
Standard Analyzer or add the synonym entry without the stop word.

|

Required  
  
`name`

|

string

|

Name of the synonym mapping. Name must be unique in the index definition.
Value can't be an empty string.

|

Required  
  
`source`

|

document

|

Source collection for synonyms. The `source` option takes the `collection`
field.

|

Required  
  
`source.collection`

|

string

|

Name of the MongoDB collection that is in the same database as the Atlas
Search index. Documents in this collection must be in the format described in
the Synonyms Source Collection Documents.

|

Required  
  
## Synonyms Source Collection Documents

Each document in the collection specified as the source for the synonyms
describe how one or more words map to one or more synonyms of those words.

## Note

On free and shared tier Atlas clusters, the synonyms collection can't exceed
10,000 documents.

### Format of Synonyms Source Collection Documents

You must configure each document with the following fields:

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`input`

|

array of strings

|

Required for `mappingType: explicit` mappings.

For `explicit` mappings, `synonyms` values are synonyms of each `input` token.
Value can't be an empty or all-whitespace string. You can specify the same
`input` value in multiple documents.

|

Conditional  
  
`mappingType`

|

string

|

Type of mapping. Value can be one of the following:

  * `equivalent` \- describes a set of tokens that are equivalent to one another. For an example of this `mappingType`, see Example.

  * `explicit` \- matches `input` tokens and replaces them with all alternative `synonyms` tokens. For an example of this `mappingType`, see Example.

|

Required  
  
`synonyms`

|

array of strings

|

Words that are synonyms of one another if `mappingType` is `equivalent` or
synonyms of `input` tokens if `mappingType` is `explicit`. `synonyms` must
have at least one value.

## Note

Atlas Search considers each string, regardless of the number of words within,
to be a single token. For example, Atlas Search tokenizes the string `sushi
chef` as a single term and doesn't return any results for a search for `sushi`
or `chef` individually.

To use synonyms with stop words, you must either add the synonym entry without
the stop word or index the field using the Standard Analyzer.

For an example of each `mappingType` see `mappingType` Examples.

|

Required  
  
The documents in the collection can contain other fields. The documents in the
collection are additive, and mappings are deduplicated. Atlas Search synonyms
are stored as a separate Atlas collection, which counts against the same
storage quota as any other collection in Atlas. Atlas Search might use more
compute resources to apply synonyms from larger synonyms source collections.

## Warning

Don't include invalid synonym documents in the synonym source collection.
Atlas Search doesn't create indexes if the indexes use synonym mappings that
reference collections with invalid documents. Only include synonym documents
that are properly formatted in your synonym source collection.

MongoDB doesn't recommend adding synonym documents to synonym source
collections in a production environment without first validating that they are
properly formatted and behave as expected in a test environment.

### Changes to Synonyms Source Collection Documents

If you make changes to your synonyms source collection:

  * You don't need to reindex because Atlas Search watches for changes and automatically updates its internal synonym map.

  * The time it takes Atlas Search to update the synonym mappings increases with the synonym source collection size. Note that the changes to synonym documents are reflected in your Atlas Search query results eventually.

### `mappingType` Examples

Atlas provides the documents for the following Atlas Search mapping type
examples in a collection named `sample_synonyms`. You can load these documents
on your cluster in the same database as your collection. To load these
documents on your cluster, when you create the index for your collection, do
the following:

  1. When you select the Configuration Method, select the Visual Editor.

  2. When you Add synonym mapping to your index, select Load sample collection from the Synonym source collection dropdown.

#### `equivalent`

## Example

In this `equivalent` mapping type example, the `synonyms` tokens `car`,
`vehicle`, and `automobile` are configured to be synonyms of one another:

    
    
    {  
      
      "mappingType": "equivalent",  
      "synonyms": ["car", "vehicle", "automobile"]  
    }  
  
For a text query for `car`, `vehicle`, or `automobile` applying a synonym
mapping that includes such a document, Atlas Search returns documents that
contain the term `car`, `vehicle`, or `automobile`.

#### `explicit`

## Example

In this `explicit` mapping type example, `input` token `beer` is configured to
consider `beer`, `brew`, and `pint` as synonyms:

    
    
    {  
      
      "mappingType": "explicit",  
      "input": ["beer"],  
      "synonyms": ["beer", "brew", "pint"]  
    }  
  
For a text query for `beer` applying a synonym mapping that includes such a
document, Atlas Search returns documents that contain the terms "beer",
"brew", or "pint" because the `input` token `beer` is explicitly mapped to all
these `synonyms` tokens. However, for a query for `pint`, Atlas Search does
not find documents that contain `beer` because `pint` is not explicitly mapped
to `beer`.

## Example

The examples on this page include:

  * A sample collection titled `user_feedback.comments`.

  * A sample synonyms source collection titled `user_feedback.synonyms`.

  * Index definition examples that rely on documents in both of these collections.

### Collection Example

`user_feedback.comments` contains the following documents:

    
    
    {  
      
      "type": "car dealer",  
      "comments": "Blue four-door sedan, lots of trunk space in the car."  
    }  
      
    
    {  
      
      "type": "winery",  
      "comments": "Beer and skittles for all."  
    }  
      
    
    {  
      
      "type": "apparel store",  
      "comments": "Beautiful apparel for the bride."  
    }  
      
    
    {  
      
      "type": "recreation rental",  
      "comments": "Sails as well as the day it was made."  
    }  
  
### Synonym Source Collection Example

The following collection titled `user_feedback.synonyms` is an example synonym
source collection for the `user_feedback.comments` collection.

## Note

To learn how to format the documents in the collection, see Synonyms Source
Collection Documents.

`user_feedback.synonyms` contains the following documents:

    
    
    {  
      
      "mappingType": "equivalent",  
      "synonyms": ["car", "vehicle", "automobile"]  
    }  
      
    
    {  
      
      "mappingType": "explicit",  
      "input": ["beer"],  
      "synonyms": ["beer", "brew", "pint"]  
    }  
      
    
    {  
      
      "mappingType": "equivalent",  
      "synonyms": ["dress", "apparel", "attire"]  
    }  
      
    
    {  
      
      "mappingType": "explicit",  
      "input": ["boat"],  
      "synonyms": ["boat", "vessel", "sail"]  
    }  
  
### Index Definition Examples

The following examples for the `user_feedback.comments` collection show the
index definitions using static and dynamic mappings.

## Note

For sample queries on the `user_feedback.comments` collection using the
following indexes, see examples in the text operator.

#### Static Mapping

The following index:

  * Configures an index with a single text field and a single synonym mapping definition that uses the mapping configured in the `user_feedback.synonyms` collection.

  * Analyzes the `comments` field with the `lucene.english` analyzer.

  * Enables synonyms from `synonyms` collection for queries over fields analyzed with the `lucene.english` analyzer.

You can use the Visual Editor or the JSON Editor in the Atlas UI to configure
the following index. To configure this index, after you select your
configuration method, select the `comments` collection in the `user_feedback`
database.

Visual Editor

JSON Editor

  1. Click Refine Your Index.

  2. In the Field Mappings section, click Add Field.

  3. Configure the following settings in the Add Field Mapping window:

Field Name

|

Enable Dynamic Mapping

|

Data Type Configuration  
  
||  
  
Select `comments`.

|

Toggle to disable.

|

    1. Click Add Data Type.

    2. Select String from the dropdown.

    3. Select `lucene.english` under `lucene.language` from the Index Analyzer dropdown.  
  
  4. Click Add.

  5. In the Synonyms Mappings section, click Add Synonym Mapping.

  6. Configure the following settings in the Add Synonym Mapping window:

Synonym mapping name

|

Synonym source collection

|

Analyzer  
  
||  
  
Enter `mySynonyms`

|

Select `synonyms`.

|

Select `lucene.english` under `lucene.language` from dropdown.  
  
  7. Click Add.

#### Dynamic Mapping

The following index:

  * Configures an index for all the fields in the documents and a single synonym mapping definition that uses the mapping configured in the `user_feedback.synonyms` collection.

  * Uses the default analyzer, `lucene.standard`, to analyze all the fields.

  * Enables synonyms from `synonyms` collection for queries over fields analyzed with the `lucene.standard` analyzer.

You can use the Visual Editor or the JSON Editor in the Atlas UI to configure
the following index. To configure this index, after you select your
configuration method, select the `comments` collection in the `user_feedback`
database.

Visual Editor

JSON Editor

  1. Click Refine Your Index.

  2. In the Synonyms Mappings section, click Add Synonym Mapping.

  3. Configure the following settings in the Add Synonym Mapping window:

Synonym mapping name

|

Synonym source collection

|

Analyzer  
  
||  
  
Enter `mySynonyms`

|

Select `synonyms`.

|

Select `lucene.standard` from the dropdown if it isn't already selected.  
  
  4. Click Add.

← Define Stored Source Fields in Your Atlas Search IndexReview Atlas Search
Index Syntax →

