Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Define Stored Source Fields in Your Atlas Search Index

Share Feedback

On this page

  * Syntax
  * Options
  * Boolean Values
  * Object
  * Examples

The `storedSource` option in an Atlas Search index definition specifies the
fields in the source document that Atlas Search must store. Atlas Search
doesn't index stored fields and so you can't query these fields, but you can
retrieve stored fields at query time using the returnStoredSource option. In
certain cases, this configuration improves query performance by avoiding
implicit query time lookup on the backend database. You can store fields of
all Data Types on Atlas Search.

## Note

`storedSource` is only available on Atlas clusters running one of the
following versions:

  * MongoDB 4.4.12+

  * MongoDB 5.0.6+

  * MongoDB 6.0+

To learn more about retrieving the stored fields, see Return Stored Source
Fields.

## Syntax

The `storedSource` option has the following syntax in an index definition:

    
    
    {  
      
      ...,  
      "storedSource": true | false | {  
        "include" | "exclude": [  
          "<field-name>",  
          ...  
        ]  
      }  
    }  
  
## Options

The `storedSource` option takes a boolean value or an object in the index
definition.

### Boolean Values

Value

|

Description  
  
|  
  
`true`

|

Specifies that Atlas Search must store all the fields in the documents.
Storing full documents might significantly impact performance during indexing
and querying. To learn more, see Storing Source Fields.  
  
`false`

|

Specifies that Atlas Search must not store the original source document. This
is the default value for the `storedSource` option.  
  
### Object

The `storedSource` option object accepts one of the following fields:

## Note

The object must contain either `include` or `exclude`.

Field

|

Type

|

Description  
  
||  
  
`include`

|

array of strings

|

List that contains the field names or dot-separated paths to fields to store.
In addition to the specified fields, Atlas Search stores `_id` also by
default.  
  
`exclude`

|

array of strings

|

List that contains the field names or dot-separated paths to fields to exclude
from being stored. If specified, Atlas Search stores original documents except
the fields listed here.  
  
## Examples

The following index examples use the fields in the `sample_mflix.movies`
collection to demonstrate how to configure the fields to store on Atlas Search
using the `storedSource` option. You can use the Visual Editor or the JSON
Editor in the Atlas UI to configure the indexes.

Store Specified

Exclude Specified

Store All Fields

## Example

The following example stores only the `title` and `awards.wins` fields in the
documents in the collection. After you select your preferred configuration
method, select the `movies` collection under the `sample_mflix` database.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Stored Source Fields section, click Specified.

  3. Select `awards.wins` from the dropdown in the Field Name column and click Add.

  4. Click Add Field to specify another field to store.

  5. Select `title` from the dropdown in the Field Name column and click Add.

  6. Click Save Changes.

← How to Index String Fields For Faceted SearchDefine Synonym Mappings in Your
Atlas Search Index →

