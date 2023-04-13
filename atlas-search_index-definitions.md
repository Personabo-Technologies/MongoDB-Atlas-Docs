Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review Atlas Search Index Syntax

Share Feedback

On this page

  * Syntax
  * Options

Atlas Search can index data in different ways. When you define an Atlas Search
index, you can specify a particular analyzer or multiple analyzers to index
certain fields. To learn more, see Process Data with Analyzers. You can also
index certain fields and omit others, or you can dynamically index all the
fields in a collection. To learn more, see Define Field Mappings. You can
define Atlas Search indexes through the Atlas User Interface, Atlas Search
API, and Atlas CLI.

This page describes the JSON syntax and fields for an Atlas Search index.

## Important

If you use the $out aggregation stage to modify a collection with an Atlas
Search index, you must delete and re-create the search index. If possible,
consider using $merge instead of `$out`.

## Syntax

Basic

Expanded

    
    
    1| {   
    |  
    2|   "name": "<index-name>",   
    3|   "mappings": {   
    4|     "dynamic": <boolean>,   
    5|     "fields": { <field-definition> }   
    6|   }  
    7| }  
    8|     
  
## Options

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`analyzer`

|

string

|

Optional

|

Specifies the analyzer to apply to string fields when indexing. If you set
this only at the top and do not specify an analyzer for the fields in the
index definition, Atlas Search applies this analyzer to all the fields. To use
a different analyzer for each field, you must specify a different analyzer for
the field. If omitted, defaults to Standard Analyzer.  
  
`analyzers`

|

array of Custom Analyzers

|

Optional

|

Specifies the Custom Analyzers to use in this index.  
  
`mappings`

|

Document Field Definition

|

Required

|

Specifies how to index fields at different paths for this index.  
  
`mappings.dynamic`

|

boolean

|

Optional

|

Enables or disables dynamic mapping of fields for this index.

If set to `true`, Atlas Search recursively indexes all dynamically indexable
fields.

If set to `false`, you must specify individual fields to index using
`mappings.fields`.

If omitted, defaults to `false`.

## Important

Atlas Search dynamically indexes all fields in a `document` using the default
settings for the detected data type. Atlas Search also dynamically indexes all
nested documents under the `document`, unless you explicitly override by
setting `dynamic` to `false`.

To learn more, see index configuration example.  
  
`mappings.fields`

|

document

|

Conditional

|

Required only if dynamic mapping is disabled.

Specifies the fields that you would like to index. To learn more, see Define
Field Mappings.  
  
`name`

|

string

|

Optional

|

Specifies a name for the index. In each namespace, names of all indexes in the
namespace must be unique. If omitted, defaults to `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.  
  
`searchAnalyzer`

|

string

|

Optional

|

Specifies the analyzer to apply to query text before searching with it. If
omitted, defaults to the analyzer that you specify for the `analyzer` option.
If you omit both the `searchAnalyzer` and the `analyzer` options, defaults to
the Standard Analyzer.  
  
`storedSource`

|

boolean or Stored Source Definition

|

Optional

|

Specifies fields in the documents to store for query-time look-ups using the
returnedStoredSource option. You can store fields of all Data Types on Atlas
Search. Value can be one of the following:

  * `true`, to store all fields

  * `false`, to not store any fields

  * Object that specifies the fields to `include` or `exclude` from storage

If omitted, defaults to `false`. To learn more about the syntax and fields,
see Define Stored Source Fields in Your Atlas Search Index.

## Note

`storedSource` is only available on Atlas clusters running one of the
following versions:

  * MongoDB 4.4.12+

  * MongoDB 5.0.6+

  * MongoDB 6.0+

  
  
`synonyms`

|

array of Synonym Mapping Definition

|

Optional

|

Synonym mappings to use in your index. To learn more, see Define Synonym
Mappings in Your Atlas Search Index.  
  
← Define Synonym Mappings in Your Atlas Search IndexResume or Delete an Atlas
Search Index Draft →

