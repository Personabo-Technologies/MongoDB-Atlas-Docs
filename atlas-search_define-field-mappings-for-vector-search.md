Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Define Field Mappings

Share Feedback

On this page

  * Static and Dynamic Mappings
  * BSON Data Types
  * Atlas Search Field Types
  * knnVector

When you create an Atlas Search index, you can explicitly specify the fields
to index using static mappings. For the fields in the collection that you want
to index, you must include a `type` field that describes the data type of the
field in the field definition. You can specify an array of field definitions
for a field, one for each data type.

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
  
Alternatively, you can configure Atlas Search to automatically index all the
supported field types in the collection using dynamic mappings.

## Note

Unlike compound indexes, the order of fields in the Atlas Search index
definition is not important. Fields can be defined in any order.

## Static and Dynamic Mappings

For **Static mappings** , set `mappings.dynamic` to `false` and specify the
fields to index using `mappings.fields`. Atlas Search only indexes the
specified fields with specific options.

Use static mappings to configure index options for fields that shouldn't be
indexed dynamically, or to configure a single field independently from others
in an index.

## Note

You must specify static mappings when `mappings.dynamic` is `false`.

For **Dynamic mappings** , set `mappings.dynamic` to `true`. Atlas Search
automatically indexes the fields of supported types in each document.

Use dynamic mappings if your schema changes regularly or is unknown, or when
experimenting with Atlas Search. You can configure an entire index to use
dynamic mappings, or specify individual fields, such as fields of type
`document`, to be dynamically mapped.

## Note

Dynamically mapped indexes occupy more disk space than statically mapped
indexes and may be less performant.

## BSON Data Types

Atlas Search doesn't support the following BSON data types:

  * Binary Data

  * Decimal128

  * JavaScript code with scope

  * Max key

  * Min key

  * Null

  * Regular Expression

  * Timestamp

The following table lists the supported BSON data types and the Atlas Search
field type for the BSON data types. The table also indicates whether the field
type is automatically indexed when you enable dynamic mappings.

BSON Type

|

Atlas Search Field Type

|

Dynamic Indexing?  
  
||  
  
Array

|

|  
  
Boolean

|

boolean

|  
  
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
  
Double

|

knnVector

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
  
32-bit integer

|

knnVector

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
  
64-bit integer

|

knnVector

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

How to Index Fields for Autocompletion

|  
  
## Note

You can store fields of all supported Data Types on Atlas Search using the
`storedSource` option.

## Atlas Search Field Types

### knnVector

Use the `knnVector` type to index vector embeddings. The vector field should
be represented as an array of numbers (BSON `int32`, `int64`, or `double` data
types only).

## Note

This feature is in early access and available only for evaluation purposes, to
validate functionality, and to gather feedback from a small closed group of
early access users. It is not recommended for production deployments as we may
introduce breaking changes. This feature doesn't include formal consulting,
SLAs, or technical support obligations.

The `knnVector` type has the following options:

Option

|

Type

|

Necessity

|

Purpose  
  
|||  
  
`type`

|

string

|

Required

|

Human-readable label that identifies this field type. Value must be
`knnVector`.  
  
`dimensions`

|

int

|

Required

|

Number of vector dimensions, which Atlas Search enforces at index- and query-
time. This value can't be greater than `1024`.  
  
`similarity`

|

string

|

Required

|

Vector similarity function to use to search for top K-nearest neighbors. Value
can be one of the following:

  * `euclidean` \- measures the distance between ends of vectors. This allows you to measure similarity based on varying dimensions. To learn more, see Euclidean.

  * `cosine` \- measures similarity based on the angle between vectors. This allows you to measure similarity that isn't scaled by magnitude. You can't use zero magnitude vectors with `cosine`. To measure cosine similarity, we recommend that you normalize your vectors and use `dotProduct` instead. To learn more, see Cosine.

  * `dotProduct` \- measures similar to `cosine`, but takes into account the magnitude of the vector. This allows you to efficiently measure similarity based on both angle and magnitude. To use `dotProduct`, you must normalize the vector to unit length at index- and query-time. To learn more, see Dot Product.

## Note

If you normalize the magnitude, `cosine` and `dotProduct` are almost identical
in measuring similarity.  
  
## Example

Consider a collection named `cheese_varieties` with the following documents:

    
    
    {  
      
      "_id": 1,  
      "name": "mozzarella",  
      "description": "Italian cheese typically made from buffalo's milk.",  
      "countryOfOrigin": "Italy",  
      "egVector": [-0.09950768947601318,-0.02402166835963726,-0.046839360147714615,0.06274440884590149,-0.0920015424489975],  
      "aging": "none",  
      "yearProduced": 2022,  
      "brined": false  
    }  
      
    
    {  
      
      "_id": 2,  
      "name": "parmesan",  
      "description": "Italian hard, granular cheese produced from cow's milk.",  
      "countryOfOrigin": "Italy",  
      "egVector": [-0.04228218272328377,-0.024080513045191765,-0.029374264180660248,-0.04369240626692772,-0.01295427419245243],  
      "aging": "at least 1 year",  
      "yearProduced": 2021,  
      "brined": false  
    }  
      
    
    {  
      
      "_id": 3,  
      "name": "feta",  
      "description": "Greek brined white cheese made from sheep's milk or from a mixture of sheep and goat's milk.",  
      "countryOfOrigin": "Greece",  
      "egVector": [-0.015739429742097855,0.04937680810689926,-0.1067470908164978,0.1293928325176239,-0.03162907809019089],  
      "aging": "about 3 months",  
      "yearProduced": 2021,  
      "brined": true  
    }  
  
The following index definition for the `cheese_varieties` collection
dynamically indexes all the dynamically indexable fields in the collection and
statically indexes `egVector` as a `knnVector` type. The index definition also
specifies `5` vector dimensions and measures similarity using `euclidean`.

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "dynamic": true,  
    4|     "fields": {  
    5|       "egVector": {  
    6|         "type": "knnVector",  
    7|         "dimensions": 5,  
    8|         "similarity": "euclidean"  
    9|       }  
    10|     }  
    11|   }  
    12| }  
  
If you add the `cheese_varieties` collection to a database on your cluster and
create the preceding Atlas Search index for this collection, you can run
knnBeta queries against this collection. To learn more about the sample
queries that you can run, see Examples.

