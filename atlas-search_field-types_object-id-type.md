Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index ObjectId Values in Fields

Share Feedback

On this page

  * Define the Index for the `objectId` Type
  * Configure `objectId` Field Properties
  * Try an Example for the `objectId` Type

You can use the Atlas Search `objectId` type to index ObjectId values. You can
query fields of type `objectId` using the equals operator.

You can also use the `objectId` type to index:

  * Fields whose value is an array of `objectId`. To learn more, see How to Index the Elements of an Array.

  * `objectId` fields inside an array of documents indexed as the embeddedDocuments type.

If you enable dynamic mappings, Atlas Search automatically indexes fields of
type `objectId`. You can use the **Visual Editor** or the **JSON Editor** in
the Atlas UI to index fields as the `objectId` type.

## Define the Index for the `objectId` Type

To define the index for the `objectId` type, choose your preferred
configuration method in the Atlas UI and then select the database and
collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select ObjectId. To learn more more about this type, see Field Properties.

  5. Click Add.

## Configure `objectId` Field Properties

The Atlas Search `objectId` type takes the following option:

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
`objectId`.  
  
## Try an Example for the `objectId` Type

The following index definition example uses the sample_mflix.comments
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

The following example index definition indexes the `movie_id` field as the
`objectId` data type to support queries against that field using the Atlas
Search equals operator.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select movie_id from the Field Name dropdown.

  2. Click the Data Type dropdown and select ObjectId.

  3. Click Add.

## Tip

### See also: Additional Index Definition Examples

  * equals Operator

← How to Index Numeric Values for Faceted SearchHow to Index String Fields →

