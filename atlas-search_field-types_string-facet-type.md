Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index String Fields For Faceted Search

Share Feedback

On this page

  * Define the Index for the `stringFacet` Type
  * Configure Properties for the `stringFacet` Type
  * Try an Example for the `stringFacet` Type

You can use the Atlas Search `stringFacet` type to index string fields for
faceting, which allows you to run a facet query on that field. Atlas Search
doesn't apply the analyzer when indexing `string` fields for faceting.

Atlas Search only supports facet queries against fields indexed as the
`stringFacet` type. To perform a normal search also on the same field, you
must index the field as type `string` also.

Atlas Search doesn't dynamically index `string` values for faceting. You must
use static mappings to index `string` values for faceting. You can use the
**Visual Editor** or the **JSON Editor** in the Atlas UI to index date fields
as the `stringFacet` type.

## Define the Index for the `stringFacet` Type

To define the index for the `stringFacet` type, choose your preferred
configuration method in the Atlas UI and then select the database and
collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select StringFacet. To learn more more about this type, see Field Properties.

  5. Click Add.

## Configure Properties for the `stringFacet` Type

The Atlas Search `stringFacet` type has the following parameters:

UI Field Name

|

JSON Option

|

Type

|

Necessity

|

Description  
  
||||  
  
Data Type

|

`type`

|

string

|

Required

|

Human-readable label that identifies this field type. Value must be
`stringFacet`.  
  
## Try an Example for the `stringFacet` Type

The following index definition example uses the sample_mflix.movies
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

stringFacet Type Example

Multiple Types Example

The following index definition for the `sample_mflix.movies` collection in the
sample dataset indexes the `genres` field as `stringFacet` for faceting.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select genres from the Field Name dropdown.

  2. Click the Data Type dropdown and select StringFacet.

  3. Click Add.

## Tip

### See also: Additional Index Definition Examples

  * facet Collector

  * facet Tutorial

← How to Index String FieldsDefine Stored Source Fields in Your Atlas Search
Index →

