Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Index the Elements of an Array

Share Feedback

On this page

  * How Does Atlas Search Index Array Elements?
  * How Can I Index Objects in Arrays?
  * Review the Limitations
  * Define the Index for the Array Elements
  * Try an Example for Indexing Array Elements

For indexing arrays, Atlas Search requires only the data type of the array
elements. You don't have to specify that the data is contained in an array
(`[]`) in the index definition.

If you enable dynamic mappings, Atlas Search automatically indexes elements of
dynamically indexable data types inside the array. To learn more about the
data types that Atlas Search dynamically indexes, see Data Types.

You can use the **Visual Editor** or the **JSON Editor** in the Atlas UI to
define the index for elements in arrays.

## How Does Atlas Search Index Array Elements?

Atlas Search indexes the supported data types inside an array by flattening
the fields during indexing.

## Example

Consider the following documents:

    
    
    doc1 = { a: {b: [[<value1>, <value2>], <value3>] }}  
      
    doc2 = { a: {b: [<value1>, <value2>, <value3>] } }  
    doc3 = { a: [{ b: <value1>}, {b: <value2>}, {b: <value3>}] }  
  
Atlas Search flattens the preceding arrays similar to the following during
indexing:

    
    
    LuceneDoc<n> = {"a.b":[<value1>,<value2>,<value3>]}  
      
  
## How Can I Index Objects in Arrays?

To query fields inside an array of documents or objects, you must use the
embeddedDocuments type to index the field that contains the array of objects.

## Review the Limitations

Atlas Search doesn't index the following Atlas Search field types if the field
type is contained in an array or is in a document that is contained in an
array:

  * dateFacet

  * numberFacet

## Define the Index for the Array Elements

To define the index for the array elements, choose your preferred
configuration method in the Atlas UI and then select the database and
collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field Mapping to open the Add Field Mapping window.

  3. Select the field of type array to index from the Field Name dropdown.

  4. Click the Data Type dropdown and select the data type of the array element that you want to index. To learn more about the configuring the properties for the selected type, refer to the documentation for the selected type.

  5. Click Add.

## Try an Example for Indexing Array Elements

The following index definition example uses the sample_mflix.movies
collection. If you have the sample data already loaded on your cluster, you
can use the Visual Editor or JSON Editor in the Atlas UI to configure the
index. After you select your preferred configuration method, select the
database and collection, and refine your index to add field mappings.

The following index definition indexes the `genres` field, which contains an
array of string values.

Visual Editor

JSON Editor

  1. In the Add Field Mapping window, select genres from the Field Name dropdown.

  2. Click the Data Type dropdown and select String.

  3. Keep the default settings for the String Properties.

  4. Click Add.

← Define Field MappingsHow to Index Fields for Autocompletion →

