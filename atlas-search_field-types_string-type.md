Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index String Fields

Share Feedback

On this page

  * Review the Limitations for the `string` Type
  * Define the Index for the `string` Type
  * Configure `string` Field Properties
  * Try an Example for the `string` Type

You can use the Atlas Search `string` type to index string fields. You can use
the Atlas Search phrase, queryString, span, text, wildcard, regex, and
moreLikeThis operators to query fields indexed as the `string` type.

If you enable dynamic mappings, Atlas Search automatically indexes fields of
type `string`. You can use the **Visual Editor** or the **JSON Editor** in the
Atlas UI to index fields as the `string` type.

## Review the Limitations for the `string` Type

You can't use the Atlas Search `string` type to index fields for facet or
autocomplete queries. Instead, you must use static mappings to index the
string fields as the following types:

  * stringFacet type to run a facet query on string fields. Note that Atlas Search doesn't dynamically index string fields for faceting.

  * autocomplete type to run autocomplete operator queries on string fields. Note that Atlas Search doesn't dynamically index string fields for autocompletion.

## Define the Index for the `string` Type

To define the index for the `string` type, choose your preferred configuration
method in the Atlas UI and then select the database and collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select String.

  5. (Optional) Expand and configure the String Properties for the field. To learn more, see Configure `string` Field Properties.

  6. (Optional) Click Add Multi Field to configure the following alternate analyzer settings for that field:

    1. Enter a name for the alternate analyzer in the Multi Field Name field.

    2. Configure the string field properties for the alternate analyzer under Multi Field Properties. To learn more, see Configure `string` Field Properties.

    3. (Optional) Click Add Another Mult Field and repeat steps **1** and **b** to configure more analyzers for the field.

  7. Click Add.

## Configure `string` Field Properties

The Atlas Search `string` type takes the following parameters:

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

Required

|

Human-readable label that identifies this field type. Value must be `string`.

|  
  
`analyzer`

|

string

|

Optional

|

Name of a built-in or overridden analyzer to use for indexing the field. If
omitted, defaults to an analyzer in the following order:

  1. The `analyzer` option for the index if specified.

  2. The `lucene.standard` analyzer.

|  
  
`searchAnalyzer`

|

string

|

Optional

|

Analyzer to use when querying the field. If omitted, defaults to an analyzer
in the following order:

  1. The `analyzer` option for this field if specified.

  2. The `searchAnalyzer` option for the index if specified.

  3. The `analyzer` option for the index if specified.

  4. The `lucene.standard` analyzer.

|  
  
`indexOptions`

|

string

|

Optional

|

Amount of information to store for the indexed field. Value can be one of the
following:

  * `docs` \- Only indexes documents. The frequency and position of the indexed term are ignored. Only a single occurence of the term is reflected in the score.

  * `freqs` \- Only indexes documents and term frequency. The position of the indexed term is ignored.

  * `positions` \- Indexes documents, term frequency, and term positions.

  * `offsets` \- (Default) Indexes documents, term frequency, term positions, and term offsets. This option is required for highlight.

|

`offsets`  
  
`store`

|

boolean

|

Optional

|

Flag that indicates whether to store the exact document text as well as the
analyzed values in the index. Value can be `true` or `false`. The value for
this option must be `true` for highlight.

## Note

To reduce the index size and performance footprint, we recommend setting
`store` to `false`. To learn more, see Atlas Search Index Performance.

|

`true`  
  
`ignoreAbove`

|

int

|

Optional

|

Maximum number of characters in the value of the field to index. Atlas Search
doesn't index if the field value is greater than the specified number of
characters.

|  
  
`multi`

|

String Field Definition

|

Optional

|

String field to index with the name of the alternate analyzer specified in the
`multi` object. To learn more about specifying the `multi` object, see Multi
Analyzer and example below.

|  
  
`norms`

|

string

|

Optional

|

String that specifies whether to include or omit the field length in the
result when scoring. The length of the field is determined by the number of
tokens produced by the analyzer for the field. Value can be one of the
following:

  * `include` \- to include the field length when scoring.

  * `omit` \- to omit the field length when scoring.

If value is `include`, Atlas Search uses the length of the field to determine
the higher score when scoring. For example, if two documents match an Atlas
Search query, the document with the shorter field length scores higher than
the document with the longer field length.

If value is `omit`, Atlas Search ignores the field length when scoring.

|

`include`  
  
## Try an Example for the `string` Type

The following index definition example uses the sample_mflix.movies
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

Basic Example

Multi Example

The following index definition indexes string values in the `title` field as
Atlas Search `string` type:

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select title from the Field Name dropdown.

  2. Click the Data Type dropdown and select String.

  3. Review the default settings for the String Properties.

  4. Click Add.

← How to Index ObjectId Values in FieldsHow to Index String Fields For Faceted
Search →

