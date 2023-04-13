Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index Fields in Arrays of Objects and Documents

Share Feedback

On this page

  * Review `embeddedDocuments` Type Limitations
  * Define the Index for the `embeddedDocument` Type
  * Configure `embeddedDocument` Field Properties
  * Try an Example for the `embeddedDocument` Type

## Note

The Atlas Search embeddedDocuments index option, embeddedDocument operator,
and `embedded` scoring option are in preview. When an Atlas Search index on a
replica set or single MongoDB shard reaches Lucene's two billion document
limit, Atlas Search doesn't index new documents or apply updates to existing
documents for that index. A solution to accommodate this limitation will be in
place when this feature is generally available. To troubleshoot any issues
related to using this feature, contact Support.

You can use the Atlas Search `embeddedDocuments` type to index fields in
documents and objects that are elements of an array. Atlas Search indexes
embedded documents independent of their parent document. Each indexed document
contains only fields that are part of the embedded document array element. You
can use only the embeddedDocument operator to query fields indexed as
`embeddedDocuments` type.

Atlas Search doesn't dynamically index fields of type `embeddedDocument`. You
_must_ use static mappings to index `embeddedDocument` fields. You can use the
**Visual Editor** or the **JSON Editor** in the Atlas UI to index fields of
type `embeddedDocument`.

## Review `embeddedDocuments` Type Limitations

The following limitations apply:

  * You can use `embeddedDocuments` only on fields with up to `5` levels of nesting. An `embeddedDocuments` field can't have more than `4` parent `embeddedDocuments` fields.

  * You can't use `embeddedDocuments` for date or numeric faceting.

  * You can't highlight fields or children of fields indexed as the `embeddedDocuments` type.

  * Atlas Search doesn't support indexing more than two billion index objects, where each indexed embedded document counts as a single object. Using the `embeddedDocuments` field type can result in indexing objects over this limit, which causes an index to transition to a failed state. If your collection has large arrays that might generate two billion objects, you must shard any clusters that contain indexes with the `embeddedDocuments` type.

## Define the Index for the `embeddedDocument` Type

To define the index for the `embeddedDocument` type, choose your preferred
configuration method in the Atlas UI and then select the database and
collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select EmbeddedDocument.

  5. Toggle the Enable Dynamic Mapping setting to enable or disable dynamic indexing of all dynamically indexable fields in the document. To learn more, see Configure `document` Field Properties.

  6. Click Add.

  7. If you disabled dynamic mapping, click Add Embedded Field for the EmbeddedDocument type field to define field mappings for the fields in the document.

## Configure `embeddedDocument` Field Properties

The Atlas Search `embeddedDocuments` type takes the following parameters:

Field

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

Human-readable label that identifies the field type. Value must be
`embeddedDocuments`.

|  
  
`dynamic`

|

boolean

|

Optional

|

Flag that specifies whether to index every dynamically indexable field in the
document. Value can be one of the following:

  * `true` \- index all indexable fields.

  * `false` \- don't index all the indexable fields.

|

`false`  
  
`fields`

|

document

|

Conditional

|

Fields to index.

If `dynamic` is `true`, Atlas Search indexes all indexable fields.

If `dynamic` is `false`, you can specify the fields to index in the field
definition for `fields`.

## Note

Atlas Search doesn't support indexing facet fields as part of an
`embeddedDocuments` field.

|

`{}`  
  
## Try an Example for the `embeddedDocument` Type

The following index definition example uses the sample_supplies.sales
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

Index All Fields

Index Specified Fields Only

The following index definition indexes the array of objects in the `items`
field. It also configures Atlas Search to automatically index all dynamically
indexable fields inside the objects in the `items` array.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select items from the Field Name dropdown.

  2. Click the Data Type dropdown and select EmbeddedDocuments.

  3. Toggle Enable Dynamic Mapping to enable dynamic mapping, if needed.

  4. Click Add.

## Note

To index all fields in an embedded document including fields that Atlas Search
doesn't dynamically index, define the fields in the index definition. For
string faceting, Atlas Search counts string facets once for each document in
the result set.

For example, the following index definition configures Atlas Search to
automatically index all dynamically indexable fields inside the objects in the
`items` array. It also configures the `purchaseMethod` field inside the array
of objects to be indexed as stringFacet, which Atlas Search doesn't
dynamically index, to support Atlas Search facet queries against that field:

Visual Editor

JSON Editor

Click Add Field in the Field Mappings section and add the following fields by
clicking Add after configuring the settings for each field in the Add Field
Mapping window.

Field Name

|

Data Type  
  
|  
  
`items`

|

Click the dropdown and select `EmbeddedDocuments`.  
  
`purchaseMethod`

|

Click the dropdown and select `StringFacet`.  
  
## Tip

### See also: Additional Index Definition Examples

  * embeddedDocument Operator

  * embeddedDocument Tutorial

← How to Index Fields in Objects and DocumentsHow to Index GeoJSON Objects →

