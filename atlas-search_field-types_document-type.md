Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index Fields in Objects and Documents

Share Feedback

On this page

  * Review `document` Type Limitations
  * Define the Index for the `document` Type
  * Configure `document` Field Properties
  * Try an Example for the `document` Type

You can use the Atlas Search `document` type to index fields in objects or
documents.

If you enable dynamic mappings, Atlas Search automatically indexes fields of
type `document`. You can use the **Visual Editor** or the **JSON Editor** in
the Atlas UI to index fields as the `document` type.

## Review `document` Type Limitations

You can't use the Atlas Search `document` type to index fields in objects or
documents that are inside an array. Instead, use the Atlas Search
embeddedDocuments type to index fields in objects or documents that are
elements of an array.

## Define the Index for the `document` Type

To define the index for the `document` type, choose your preferred
configuration method in the Atlas UI and then select the database and
collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select Document.

  5. Toggle the Enable Dynamic Mapping setting to enable or disable dynamic indexing of all dynamically indexable fields in the document. To learn more, see Configure `document` Field Properties.

  6. Click Add.

  7. If you disabled dynamic mapping, click Add Child Field for the Document type field to define field mappings for the fields in the document.

## Configure `document` Field Properties

The Atlas Search `document` type takes the following parameters:

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

Human-readable label that identifies the field type. Value must be `document`.

|  
  
`dynamic`

|

boolean

|

Conditional

|

Flag that indicates whether Atlas Search recursively indexes all fields and
embedded documents. If set to `true`, Atlas Search recursively indexes all
fields and embedded documents in the `document` except fields of certain data
types.

To index all fields in a document including fields that Atlas Search doesn't
dynamically index, define the fields in the index definition.

If omitted or set to `false`, you must specify individual fields to index.

## Important

Atlas Search dynamically indexes all fields in a `document` using the default
settings for the detected data type. Atlas Search also dynamically indexes all
nested documents under the `document`, unless you explicitly override by
setting `dynamic` to `false`.

|

false  
  
`fields`

|

document

|

Conditional

|

Document that maps field names to field definitions. To learn more, see an
example. This is required if `dynamic` is omitted or set to `false`.

|  
  
## Try an Example for the `document` Type

The following index definition example uses the sample_mflix.movies
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

The index definition indexes the `awards` field as the `document` type. It
also configures Atlas Search to automatically index all the dynamically
indexable fields inside the `awards` object.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select awards from the Field Name dropdown.

  2. Click the Data Type dropdown and select Document.

  3. Toggle the Enable Dynamic Mapping setting to enable dynamic indexing of all dynamically indexable fields in the document, if it isn't already enabled.

  4. Click Add.

## Tip

### See also: Additional Index Definition Examples

  * Combined Mapping Example

← How to Index Date Fields For Faceted SearchHow to Index Fields in Arrays of
Objects and Documents →

