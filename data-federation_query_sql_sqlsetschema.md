Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `sqlSetSchema`

Share Feedback

On this page

  * Syntax
  * Parameters
  * Output
  * Examples
  * Set Schema Example
  * Delete Schema Example

The `sqlSetSchema` command sets or deletes the schema for a collection or
view. The command uses the provided schema to create the relational schema.
The command does not validate the schema provided with the command against the
data in the collection.

## Syntax

Set Schema

Delete Schema

    
    
    db.runCommand({sqlSetSchema: "<collection-name>|<view-name>", schema: {"version": 1, "jsonSchema": <jsonSchema>})  
      
  
## Parameters

Parameter

|

Type

|

Description

|

Necessity  
  
|||  
  
`<collection-name>`

|

string

|

Name of the collection for which to set the schema. Either the collection name
or view name is required.

|

Conditional  
  
`<view-name>`

|

string

|

Name of the view for which to set the schema. Either the view name or
collection name is required.

|

Conditional  
  
`schema`

|

document

|

The format version of the schema and the JSON schema to set the schema for the
collection or view or an empty document to remove the schema for the
collection or view.

## Note

You can provide a single document or an array of documents in the `items`
field. When you retrieve the schema, `items` shows the form that you used to
set the schema.

|

Required  
  
## Output

The command returns the following output if the command succeeds.

    
    
    { "ok" : 1 }  
      
  
You can verify that the command succeeded by running the `sqlGetSchema`
command. The `sqlGetSchema` command `metadata.description` should contain the
following value:

    
    
    "set using sqlSetSchema"  
      
  
## Examples

Consider a collection named `egData` in a database named `sampleDB` with the
following documents:

    
    
    {"a": {"b": {"c": [1, 2, 3]}}, "s": 1}  
      
    {"a": {"b": {"c": [4, 5, 6]}}, "s": 2}  
    {"a": {"b": [7, 8, 9]}, "s": 3}  
    {"a": {"b": {"c": []}}, "s": 4}  
    {"a": {"b": {"c": "hello"}}, "s": 5}  
    {"a": {"b": {"c": {"d": 1}}}, "s": 6}  
    {"a": {"b": {"c": null}}}  
    {"s": 7}  
  
The examples below use the `sqlSetSchema` command to set and remove schema for
the above collection.

### Set Schema Example

The following `sqlSetSchema` command sets the schema for the `egData`
collection.

    
    
    db.runCommand({sqlSetSchema : "egData", "schema" : { "version" : NumberLong(1), "jsonSchema" : { "bsonType" : [ "object" ], "properties" : { "a" : { "bsonType" : [ "object" ], "properties" : { "b" : { "bsonType" : [ "object", "array" ], "properties" : { "c" : { "bsonType" : [ "array", "string", "object", "null" ], "properties" : { "d" : { "bsonType" : [ "int" ] } }, "items" : { "bsonType" : [ "int" ] } } }, "items" : { "bsonType" : [ "int" ] } } } }, "s" : { "bsonType" : [ "int", "object" ], "properties" : { "b" : { "bsonType" : [ "object" ], "properties" : { "c" : { "bsonType" : [ "object" ], "properties" : { "d" : { "bsonType" : [ "array" ], "items" : { "bsonType" : [ "string" ] } } } } } } } } } } }})  
      
  
The previous command returns the following output.

    
    
    { "ok" : 1 }  
      
  
### Delete Schema Example

The following `sqlSetSchema` command removes the schema for the `egData`
collection.

    
    
    db.runCommand({sqlSetSchema: "egData", schema: {} })  
      
  
The previous command returns the following output.

    
    
    { "ok" : 1 }  
      
  
← `sqlGenerateSchema``sqlGetSchema` →

