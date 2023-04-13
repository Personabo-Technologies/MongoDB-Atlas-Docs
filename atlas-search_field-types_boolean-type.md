Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index Boolean Values

Share Feedback

On this page

  * Define the Index for the `boolean` Type
  * Configure `boolean` Field Properties
  * Try an Example for the `boolean` Type

You can use the Atlas Search `boolean` type to index `true` and `false`
values. You can query fields of type `boolean` using the equals operator.

You can also use the `boolean` type to index:

  * Fields whose value is an array of booleans. To learn more, see How to Index the Elements of an Array.

  * Boolean fields inside an array of documents indexed as the embeddedDocuments type.

If you enable dynamic mappings, Atlas Search automatically indexes fields of
type `boolean`. You can use the **Visual Editor** or the **JSON Editor** in
the Atlas UI to index fields as the `boolean` type.

## Define the Index for the `boolean` Type

To define the index for the `boolean` type, choose your preferred
configuration method in the Atlas UI and then select the database and
collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select Boolean. To learn more more about this type, see Field Properties.

  5. Click Add.

## Configure `boolean` Field Properties

The Atlas Search `boolean` type takes the following parameter:

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

Human-readable label that identifies this field type. Value must be `boolean`.  
  
## Try an Example for the `boolean` Type

The following index definition example uses the sample_guides.planets
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

The index definition indexes the `hasRings` field in the collection as the
Atlas Search `boolean` type to support queries against that field using the
Atlas Search equals operator.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select hasRings from the Field Name dropdown.

  2. Click the Data Type dropdown and select Boolean.

  3. Click Add.

## Tip

### See also: Additional Index Definition Examples

  * equals Operator

← How to Index Fields for AutocompletionHow to Index Date Fields →

