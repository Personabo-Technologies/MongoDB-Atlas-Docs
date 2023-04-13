Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index GeoJSON Objects

Share Feedback

On this page

  * Define the Index for the `geo` Type
  * Configure `geo` Field Properties
  * Try an Example for the `geo` Type

You can use the Atlas Search `geo` type to index geographic points and shape
coordinates. For this type, the indexed field must be a GeoJSON object. You
can use the geoShape and geoWithin operators to query indexed fields of type
`geo`.

Atlas Search doesn't dynamically index fields of type `geo`. You _must_ use
static mappings to index `geo` fields. You can use the **Visual Editor** or
the **JSON Editor** in the Atlas UI to index fields of type `geo`.

## Define the Index for the `geo` Type

To define the index for the `geo` type, choose your preferred configuration
method in the Atlas UI and then select the database and collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select Geo.

  5. Configure the field properties for the `geo` type. To learn more, see Field Properties.

  6. Click Add.

## Configure `geo` Field Properties

The Atlas Search `geo` type takes the following parameters:

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

Human-readable label that identifies this field type. UI value must be `Geo`
and JSON value must be `geo`.

|  
  
`indexShapes`

|

boolean

|

Optional

|

Flag that indicates whether to index shapes. By default, Atlas Search:

  * Indexes points, even when nested.

  * Doesn't index shape geometries such as lines and polygons.

Value can be:

  * `true` to index shapes and points

  * `false` to index only points

|

`false`  
  
## Try an Example for the `geo` Type

The following index definition example uses the
sample_airbnb.listingsAndReviews collection. If you have the sample data
already loaded on your cluster, you can use the Visual Editor or JSON Editor
in the Atlas UI to configure the index. After you select your preferred
configuration method, select the database and collection, and refine your
index to add field mappings.

The following index definition indexes the `address.location` field as the
`geo` type to support queries against that field using the Atlas Search
geoShape and geoWithin operators.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select address.location from the Field Name dropdown.

  2. Click the Data Type dropdown and select Geo.

  3. Modify the Geo Properties to set the value for Index Shapes to `true`.

  4. Click Add.

## Tip

### See also: Additional Index Definition Examples

  * geoShape Operator

  * geoWithin Operator

  * geo Tutorial

← How to Index Fields in Arrays of Objects and DocumentsHow to Index Numeric
Values →

