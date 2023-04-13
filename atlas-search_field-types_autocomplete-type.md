Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index Fields for Autocompletion

Share Feedback

On this page

  * Define the Index for the `autocomplete` Type
  * Configure `autocomplete` Field Properties
  * Try an Example for the `autocomplete` Type

You can use the Atlas Search `autocomplete` type to index text values in
string fields for autocompletion. You can configure an `autocomplete` type to
satisfy a variety of use cases. To learn more about the configuration options
available for the `autocomplete` type, such as tokenization strategy and
diacritic folding, see Configure `autocomplete` Field Properties. You can
query fields indexed as `autocomplete` type only using the autocomplete
operator.

You can also use the `autocomplete` type to index:

  * Fields whose value is an array of strings. To learn more, see How to Index the Elements of an Array.

  * String fields inside an array of documents indexed as the embeddedDocuments type.

## Tip

If you have a large number of documents and a wide range of data against which
you want to run Atlas Search queries using the autocomplete operator, building
this index can take some time. Alternatively, you can create a separate index
with only the `autocomplete` type to reduce the impact on other indexes and
queries while the index builds.

To learn more, see Atlas Search Index Performance Considerations.

Atlas Search doesn't dynamically index fields of type `autocomplete`. You
_must_ use static mappings to index `autocomplete` fields. You can use the
**Visual Editor** or the **JSON Editor** in the Atlas UI to index fields of
type `autocomplete`.

## Define the Index for the `autocomplete` Type

To define the index for the `autocomplete` type, choose your preferred
configuration method in the Atlas UI and then select the database and
collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select Autocomplete.

  5. Configure the field properties for the `autocomplete` type. To learn more, see Field Properties.

  6. Click Add.

## Configure `autocomplete` Field Properties

The Atlas Search `autocomplete` type takes the following parameters:

Option

|

Type

|

Necessity

|

Description

|

Default  
  
||||  
  
`type`

|

string

|

required

|

Human-readable label that identifies this field type. Value must be string.

|  
  
`analyzer`

|

string

|

optional

|

Name of the analyzer to use with this autocomplete mapping. You can use any
Atlas Search analyzer except the `lucene.kuromoji` language analyzer and the
following custom analyzer tokenizers and token filters:

  * nGram Tokenizer

  * edgeGram Tokenizer

  * daitchMokotoffSoundex Token Filter

  * nGram Token Filter

  * edgeGram Token Filter

  * shingle Token Filter

This option isn't available in the Visual Editor.

|

`lucene.standard`  
  
`maxGrams`

|

int

|

optional

|

Maximum number of characters per indexed sequence. The value limits the
character length of indexed tokens. When you search for terms longer than the
`maxGrams` value, Atlas Search truncates the tokens to the `maxGrams` length.

|

`15`  
  
`minGrams`

|

int

|

optional

|

Minimum number of characters per indexed sequence. We recommend `4` for the
minimum value. A value that is less than `4` could impact performance because
the size of the index can become very large. We recommend the default value of
`2` for `edgeGram` only.

|

`2`  
  
`tokenization`

|

enum

|

optional

|

Tokenization strategy to use when indexing the field for autocompletion. Value
can be one of the following:

  * `edgeGram` \- create indexable tokens, referred to as `grams`, from variable-length character sequences starting at the left side of the words as delimited by the analyzer used with this autocomplete mapping.

  * `rightEdgeGram` \- create indexable tokens, referred to as `grams`, from variable-length character sequences starting at the right side of the words as delimited by the analyzer used with this autocomplete mapping.

  * `nGram` \- create indexable tokens, referred to as `grams`, by sliding a variable-length character window over a word. Atlas Search creates more tokens for `nGram` than `edgeGram` or `rightEdgeGram`. Therefore, `nGram` takes more space and time to index the field. `nGram` is better suited for querying languages with long, compound words or languages that don't use spaces.

`edgeGram`, `rightEdgeGram`, and `nGram` are applied at the letter-level. For
example, consider the following sentence:

    
    
    | The quick brown fox jumps over the lazy dog.  
      
  
When tokenized with a `minGrams` value of `2` and a `maxGrams` value of `5`,
Atlas Search indexes the following sequence of characters based on the
`tokenization` value you choose:

edgeGram

rightEdgeGram

nGram

    
    
    Th  
      
    The  
    The{SPACE}  
    The q  
    qu  
    qui  
    quic  
    quick  
    ...  
  
## Note

Indexing a field for autocomplete with an `edgeGram`, `rightEdgeGram`, or
`nGram` tokenization strategy is more computationally expensive than indexing
a string field. The index takes more space than an index with regular string
fields.

`edgeGram`  
  
`foldDiacritics`

|

boolean

|

optional

|

Flag that indicates whether to include or remove diacritics from the indexed
text. Value can be one of the following:

  * `true` \- ignore diacritic marks in the index and query text. Returns results with and without diacritic marks. For example, a search for `cafè` returns results with the characters `cafè` and `cafe`.

  * `false` \- include diacritic marks in the index and query text. Returns only results that match the strings with or without diacritics in the query. For example, a search for `cafè` returns results only with the characters `cafè`. A search for `cafe` returns results only with the characters `cafe`.

|

`true`  
  
## Try an Example for the `autocomplete` Type

The following index definition example uses the sample_mflix.movies
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

Basic Example

Multiple Types Example

The following index definition example indexes only the `title` field as the
`autocomplete` type to support search-as-you-type queries against that field
using the autocomplete operator. The index definition also specifies the
following:

  * Use the standard analyzer to divide text values into terms based on word boundaries.

  * Use the `edgeGram` tokenization strategy to index characters starting at the left side of the words .

  * Index a minimum of `3` characters per indexed sequence.

  * Index a maximum of `5` characters per indexed sequence.

  * Include diacritic marks in the index and query text.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select title from the Field Name dropdown.

  2. Click the Data Type dropdown and select Autocomplete.

  3. Make the following changes to the Autocomplete Properties:

|  
  
|  
  
Max Grams

|

Set value to `5`.  
  
Min Grams

|

Set value to `3`.  
  
Tokenization

|

Select `edgeGram` from dropdown.  
  
Fold Diacritics

|

Select `false` from dropdown.  
  
  4. Click Add.

## Tip

### See also: Additional Index Definition Examples

  * autocomplete Operator

  * autocomplete Tutorial

← How to Index the Elements of an ArrayHow to Index Boolean Values →

