Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index Numeric Values for Faceted Search

Share Feedback

On this page

  * Review `numberFacet` Limitations
  * Define the Index for the `numberFacet` Type
  * Configure `numberFacet` Field Properties
  * Try an Example for the `numberFacet` Type

You can use the Atlas Search `numberFacet` type to index numeric values using
the specified `representation` for faceting. You can index numbers of BSON
types `int32`, `int64`, and `double`.

Atlas Search only supports facet queries against fields indexed as the
`numberFacet` type. To perform a normal search also on the same field, you
must index the field as type `number` also.

Atlas Search doesn't dynamically index `number` values for faceting. You must
use static mappings to index `number` values for faceting. You can use the
**Visual Editor** or the **JSON Editor** in the Atlas UI to index date fields
as the `numberFacet` type.

## Review `numberFacet` Limitations

The following limitations apply:

  * You can't index `decimal128` for faceting.

  * You can't index numeric values in arrays or in a document contained in an array for faceting.

  * You can't facet over numeric fields indexed as part of an `embeddedDocuments` field.

## Define the Index for the `numberFacet` Type

To define the index for the `numberFacet` type, choose your preferred
configuration method in the Atlas UI and then select the database and
collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select NumberFacet.

  5. Configure the field properties for the `numberFacet` type. To learn more, see Field Properties.

  6. Click Add.

## Configure `numberFacet` Field Properties

The Atlas Search `numberFacet` type takes the following parameters:

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

The type of field. Value must be `numberFacet`.

|  
  
`representation`

|

string

|

Optional

|

The data type of the field to index. Values can be one of the following BSON
types:

  * `int64` \- for indexing large integers without loss of precision and for rounding double values to integers. You can't use this type to index large double values.

  * `double` \- for indexing large double values without rounding.

To learn more, see example below.

|

`double`  
  
`indexIntegers`

|

boolean

|

Optional

|

Indicates whether to index or omit indexing `int32` and `int64` type values.
Value can be `true` or `false`. Either this or `indexDoubles` must be `true`.

|

`true`  
  
`indexDoubles`

|

boolean

|

Optional

|

Indicates whether to index or omit indexing `double` type values. Value can be
`true` or `false`. Either this or `indexIntegers` must be `true`.

|

`true`  
  
## Try an Example for the `numberFacet` Type

The following index definition example uses the sample_mflix.movies
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

Basic Example

Multiple Types Example

The following example index definition indexes the `year` field as the Atlas
Search `numberFacet` type to supports queries against that field using Atlas
Search facet.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select year from the Field Name dropdown.

  2. Click the Data Type dropdown and select NumberFacet.

  3. Accept the default values for the NumberFacet Properties.

  4. Click Add.

## Tip

### See also: Additional Index Definition Examples

See the following pages for additional index definition examples:

  * facet Collector

  * facet Tutorial

← How to Index Numeric ValuesHow to Index ObjectId Values in Fields →

