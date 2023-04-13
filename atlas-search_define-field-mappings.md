Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Define Field Mappings

Share Feedback

On this page

  * Static and Dynamic Mappings
  * Static Mappings
  * Dynamic Mappings
  * Data Types
  * Limitations
  * Index Field as Multiple Data Types
  * Examples
  * Static Mapping Example
  * Combined Mapping Example

When you create an Atlas Search index, you can:

  * Specify the fields to index using static mappings.

  * Configure Atlas Search to automatically index all supported field types using dynamic mappings.

To use static mappings, you must explicitly include the fields in the
collection that you want to index. In the `type` field, specify the data type
of the field in the field definition. Alternatively, you can specify an array
of field definitions for a field, one for each data type.

Syntax

    
    
    1| "mappings": {  
    |  
    2|   "dynamic": <boolean>,  
    3|   "fields": {  
    4|     "<field-name>": [  
    5|       {  
    6|         "type": "<field-type>",  
    7|         ...  
    8|       },  
    9|       ...  
    10|     ],  
    11|     ...  
    12|   }  
    13| }  
  
## Note

Unlike compound indexes, the order of fields in the Atlas Search index
definition is not important. Fields can be defined in any order.

## Static and Dynamic Mappings

You can use static and dynamic mappings to specify whether Atlas Search must
automatically index all the dynamically indexable fields in your collection.

### Static Mappings

Use static mappings to configure index options for fields that you _don't_
want indexed dynamically, or to configure a single field independently from
others in an index.

For static mappings, set `mappings.dynamic` to `false` and specify the fields
to index using `mappings.fields`. Atlas Search indexes only the specified
fields with specific options.

### Dynamic Mappings

Use dynamic mappings if your schema changes regularly or is unknown, or when
experimenting with Atlas Search. You can configure an entire index to use
dynamic mappings, or specify individual fields, such as fields of type
`document`, to be dynamically mapped. Before using dynamic mappings, see the
table for Data Types.

For dynamic mappings, set `mappings.dynamic` to `true`. Atlas Search
automatically indexes the fields of supported types in each document. For
fields of type string, Atlas Search stores the fields on `mongot`.

## Note

Dynamically mapped indexes occupy more disk space than statically mapped
indexes and may be less performant.

## Data Types

Atlas Search doesn't support the following BSON data types:

  * Binary Data

  * Decimal128

  * JavaScript code with scope

  * Max key

  * Min key

  * Null

  * Regular Expression

  * Timestamp

The following table enumerates the supported BSON data types and the Atlas
Search field types that you can use to index the BSON data types. The table
also indicates whether the Atlas Search field type is automatically included
in an Atlas Search index when you enable dynamic mappings.

BSON Type

|

Atlas Search Field Type

|

Dynamically Indexed  
  
||  
  
Array

|

`boolean`, `date`, `number`, `objectId`, `string`

|

✓ __  
  
Boolean

|

boolean

|

✓  
  
Date

|

date

|

✓  
  
Date

|

dateFacet

|  
  
Double

|

number

|

✓  
  
Double

|

numberFacet

|  
  
GeoJSON Object

|

geo

|  
  
32-bit integer

|

number

|

✓  
  
32-bit integer

|

numberFacet

|  
  
64-bit integer

|

number

|

✓  
  
64-bit integer

|

numberFacet

|  
  
Object

|

document

|

✓  
  
Object

|

embeddedDocuments (for array of objects)

|  
  
ObjectId

|

objectId

|

✓  
  
String

|

string

|

✓  
  
String

|

stringFacet

|  
  
String

|

autocomplete

|  
  
 __Some limitations apply. To learn more, seeHow to Index the Elements of an
Array.

## Note

You can store fields of all supported data types on Atlas Search using the
`storedSource` option.

### Limitations

Atlas Search doesn't support indexing more than two billion index objects,
where each indexed document counts as a single object. If you plan to index
fields that might exceed this limit, you must shard your cluster. If you use
the embeddedDocuments field type, Atlas Search might index objects over this
limit.

### Index Field as Multiple Data Types

To index a field as multiple types, define the types in the field definition
array for the field.

## Example

The following example shows the field definition for indexing a field as
multiple types.

    
    
    1| {  
    |  
    2|   ...  
    3|   "mappings": {  
    4|     "dynamic": <boolean>,  
    5|     "fields": {  
    6|       "<field-name>": [  
    7|         {  
    8|           "type": "<field-type>",  
    9|           ...  
    10|         },  
    11|         {  
    12|           "type": "<field-type>",  
    13|           ...  
    14|         },  
    15|         ...  
    16|       ],  
    17|       ...  
    18|     },  
    19|     ...  
    20|   }  
    21| }  
  
## Examples

### Static Mapping Example

The following index definition example uses static mappings.

  * The default index analyzer is lucene.standard.

  * The default search analyzer is lucene.standard. You can change the search analyzer if you want the query term to be parsed differently than how it is stored in your Atlas Search index.

  * The index specifies static field mappings (`dynamic`: `false`), which means fields that are not explicitly mentioned are not indexed. So, the index definition includes:

    * The `address` field, which is of type `document`. It has two embedded sub-fields, `city` and `state`.

The `city` sub-field uses the lucene.simple analyzer by default for queries.
It uses the `ignoreAbove` option to ignore any string of more than 255 bytes
in length.

The `state` sub-field uses the lucene.english analyzer by default for queries.

    * The `company` field, which is of type `string`. It uses the lucene.whitespace analyzer by default for queries. It has a `multi` analyzer named `mySecondaryAnalyzer` which uses the lucene.french analyzer by default for queries.

To learn more about `multi` analyzers, see Path Construction.

    * The `employees` field, which is an array of strings. It uses the lucene.standard analyzer by default for queries. For indexing arrays, Atlas Search only requires the data type of the array elements. You don't have to specify that the data is contained in an array in the index definition.

    
    
    {  
      
      "analyzer": "lucene.standard",  
      "searchAnalyzer": "lucene.standard",  
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "address": {  
            "type": "document",  
            "fields": {  
              "city": {  
                "type": "string",  
                "analyzer": "lucene.simple",  
                "ignoreAbove": 255  
              },  
              "state": {  
                "type": "string",  
                "analyzer": "lucene.english"  
              }  
            }  
          },  
          "company": {  
            "type": "string",  
            "analyzer": "lucene.whitespace",  
            "multi": {  
              "mySecondaryAnalyzer": {  
                "type": "string",  
                "analyzer": "lucene.french"  
              }  
            }  
          },  
          "employees": {  
            "type": "string",  
            "analyzer": "lucene.standard"  
          }  
        }  
      }  
    }  
  
### Combined Mapping Example

The following index definition example uses both static and dynamic mappings.

  * The default index analyzer is lucene.standard.

  * The default search analyzer is lucene.standard. You can change the search analyzer if you want the query term to be parsed differently than how it is stored in your Atlas Search index.

  * The index specifies static field mappings (`dynamic`: `false`), which means fields that aren't explicitly mentioned aren't indexed. So, the index definition includes:

    * The `company` field, which is of type `string`. It uses the lucene.whitespace analyzer by default for queries. It has a `multi` analyzer named `mySecondaryAnalyzer` which uses the lucene.french analyzer by default for queries. To learn more about `multi` analyzers, see Path Construction.

    * The `employees` field, which is an array of strings. It uses the lucene.standard analyzer by default for queries.

    * The `address` field, which is of type `document`. It has two embedded sub-fields, `city` and `state`. Instead of explicitly mentioning each nested field in the document, the index definition enables dynamic mapping for all the sub-fields in the document. It uses the lucene.standard analyzer by default for queries.

    
    
    {  
      
      "analyzer": "lucene.standard",  
      "searchAnalyzer": "lucene.standard",  
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "company": {  
            "type": "string",  
            "analyzer": "lucene.whitespace",  
            "multi": {  
              "mySecondaryAnalyzer": {  
                "type": "string",  
                "analyzer": "lucene.french"  
              }  
            }  
          },  
          "employees": {  
            "type": "string",  
            "analyzer": "lucene.standard"  
          },  
          "address": {  
            "type": "document",  
            "dynamic": true,  
            "analyzer": "lucene.standard"  
          }  
        }  
      }  
    }  
  
← Token FiltersHow to Index the Elements of an Array →

