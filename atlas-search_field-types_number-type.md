Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index Numeric Values

Share Feedback

On this page

  * Define the Index for the `number` Type
  * Configure `number` Field Properties
  * Try an Example for the `number` Type

You can use the Atlas Search `number` type to index fields with numeric values
of `int32`, `int64`, `dateTime`, and `double` data types. You can use the
equals, range, and near operators to query indexed fields of type `number`.

## Note

To query numeric values in arrays, you can use only the range operator.

Atlas Search doesn't automatically index numeric values for faceting. Instead,
you must index the numeric values using numberFacet to run a facet query on
number fields.

If you enable dynamic mappings, Atlas Search automatically indexes fields of
type `number`. You can use the **Visual Editor** or the **JSON Editor** in the
Atlas UI to index fields as the `number` type.

## Define the Index for the `number` Type

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select Number.

  5. Configure the field properties for the `number` type. To learn more, see Field Properties.

  6. Click Add.

## Configure `number` Field Properties

The Atlas Search `number` type has the following parameters:

UI Field Name

|

JSON Option

|

Type

|

Necessity

|

Description

|

Default  
  
|||||  
  
Data Type

|

`type`

|

string

|

Required

|

Human-readable label that identifies this field type. Value must be `number`.

|  
  
Representation

|

`representation`

|

string

|

Optional

|

Data type of the field to index. Values are:

  * `int64` \- for indexing large integers without loss of precision and for rounding double values to integers. You can't use this type to index large double values.

  * `double` \- for indexing large double values without rounding.

To learn more, see example below.

|

`double`  
  
Index Integers

|

`indexIntegers`

|

boolean

|

Optional

|

Flag that indicates whether to index or omit indexing `int32` and `int64` type
values. Value can be `true` or `false`. To learn more, see example below.

|

`true`  
  
Index Doubles

|

`indexDoubles`

|

boolean

|

Optional

|

Flag that indicates whether to index or omit indexing `double` type values.
Value can be `true` or `false`. To learn more, see example below.

|

`true`  
  
## Try an Example for the `number` Type

The following index definition examples use multiple collections in the sample
data. If you have the sample data already loaded on your cluster, you can use
the Visual Editor and JSON Editor to configure these indexes. After you select
your preferred configuration method, select the database and collection, and
refine your index to add field mappings.

Representation Example

Index Integers Example

Index Doubles Example

The following index definition for the `sample_analytics.accounts` collection
in the sample dataset indexes the `account_id` field with 64-bit integer
values. The following example also:

  * Indexes all other integer values in the `account_id` field.

  * Rounds any decimal values and indexes small double type values in the `account_id` field.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select account_id from the Field Name dropdown.

  2. Click the Data Type dropdown and select Number.

  3. Modify the Number Properties to set the following:

    * Representation to `int64`.

    * Index Integers to `true`.

    * Index Doubles to `true`.

  4. Click Add.

← How to Index GeoJSON ObjectsHow to Index Numeric Values for Faceted Search →

