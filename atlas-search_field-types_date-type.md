Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index Date Fields

Share Feedback

On this page

  * Define the Index for the `date` Type
  * Configure `date` Field Properties
  * Try an Example for the `date` Type

You can use the Atlas Search `date` type to index date values. You can query
fields of type `date` using the Atlas Search range, near, and equals
operators. To run a facet query on `date` fields, you must index the date
fields using dateFacet.

You can also use the `date` type to index:

  * Fields whose value is an array of dates. To learn more, see How to Index the Elements of an Array.

  * Date fields inside an array of documents indexed as the embeddedDocuments type.

## Note

To query indexed date values inside arrays, you must use the range operator.
You can't use the near operator to query date values stored in an array, even
if you have an Atlas Search index on the date values inside the array.

If you enable dynamic mappings, Atlas Search automatically indexes fields of
type `date`. You can use the **Visual Editor** or the **JSON Editor** in the
Atlas UI to index fields as the `date` type.

## Define the Index for the `date` Type

To define the index for the `date` type, choose your preferred configuration
method in the Atlas UI and then select the database and collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select Date. To learn more more about this type, see Field Properties.

  5. Click Add.

## Configure `date` Field Properties

The Atlas Search `date` type takes the following parameter:

Option

|

Type

|

Necessity

|

Description  
  
|||  
  
`type`

|

string

|

required

|

Human-readable label that identifies this field type. Value must be `date`.  
  
## Try an Example for the `date` Type

The following index definition example uses the sample_mflix.movies
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

Basic Example

Multiple Types Example

The following example index definition indexes the `released` field as the
Atlas Search `date` type to support queries against that field using Atlas
Search operators such as near, range, and equals.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select released from the Field Name dropdown.

  2. Click the Data Type dropdown and select Date.

  3. Click Add.

## Tip

### See also: Additional Index Definition Examples

  * equals Operator

  * near Operator

  * range Operator

  * date Tutorial

← How to Index Boolean ValuesHow to Index Date Fields For Faceted Search →

