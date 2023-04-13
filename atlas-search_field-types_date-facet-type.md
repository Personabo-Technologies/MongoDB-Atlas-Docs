Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index Date Fields For Faceted Search

Share Feedback

On this page

  * Review `dateFacet` Limitations
  * Define the Index for `dateFacet` Type
  * Configure `dateFacet` Field Properties
  * Try an Example for `dateFacet` Type

You can use the Atlas Search `dateFacet` type for indexing date values for
faceting.

Atlas Search only supports facet queries against fields indexed as the
`dateFacet` type. To perform a normal search also on the same field, you must
index the field as type date also.

Atlas Search doesn't dynamically index date values for faceting. You must use
static mappings to index date values for faceting. You can use the **Visual
Editor** or the **JSON Editor** in the Atlas UI to index date fields as the
`dateFacet` type.

## Review `dateFacet` Limitations

The following limitations apply:

  * You can't index a date field for faceting if it's inside an array or if it's inside a document in an array.

  * Atlas Search doesn't support date faceting over fields indexed as part of an `embeddedDocuments` field.

## Define the Index for `dateFacet` Type

To define the index for the `dateFacet` type, choose your preferred
configuration method in the Atlas UI and then select the database and
collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select DateFacet. To learn more more about this type, see Field Properties.

  5. Click Add.

## Configure `dateFacet` Field Properties

The Atlas Search `dateFacet` type takes the following parameter:

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

required

|

Human-readable label that identifies this field type. Value must be
`dateFacet`.  
  
## Try an Example for `dateFacet` Type

The following index definition example uses the sample_mflix.movies
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

Basic Example

Multiple Types Example

The following example index definition indexes the `released` field as the
Atlas Search `dateFacet` type to support queries against that field using
Atlas Search facet.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select released from the Field Name dropdown.

  2. Click the Data Type dropdown and select DateFacet.

  3. Click Add.

## Tip

### See also: Additional Index Definition Examples

  * facet Collector

  * facet Tutorial

← How to Index Date FieldsHow to Index Fields in Objects and Documents →

