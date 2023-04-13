Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# SQL Schema Format

Share Feedback

On this page

  * JSON Schema Format
  * Supported JSON Schema Fields

## JSON Schema Format

The schema for a collection is a document with two fields: `jsonSchema` and
`version`.

    
    
    "schema" : {  
      
            "version" : NumberLong(1),  
            "jsonSchema" : {}  
    }  
  
The `version` field represents the version of the schema format used by the
document and the value is always `1`. The `jsonSchema` field is a document
that describes the schema of the namespace.

## Supported JSON Schema Fields

Data Federation supports the following JSON schema fields:

  * `bsonType`

  * `items`

  * `properties`

## Note

You can provide a single document or an array of documents for the `items`
field. When you retrieve the schema, the `items` field shows the form that you
used for setting the schema.

To learn more about these fields, see JSON Schema Keywords.

← Schema Management`sqlGenerateSchema` →

