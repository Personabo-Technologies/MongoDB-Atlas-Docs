Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `renameCollection`

Share Feedback

On this page

  * Syntax
  * Fields
  * Output
  * Examples
  * Basic Example
  * `dropTarget` Example
  * Verify Collection
  * Troubleshoot Errors

The `renameCollection` command renames a collection to the specified new name
in the storage configuration. You can run this command only against the
`admin` database, which is the Atlas user authentication database. The command
does not support renaming collections dynamically created by the wildcard
collection function (`collectionName()`).

## Syntax

    
    
    db.runCommand({ "renameCollection": "<namespace>", "to": "<namespace>", "dropTarget": true|false })  
      
  
## Fields

Field

|

Type

|

Description

|

Required?  
  
|||  
  
`renameCollection`

|

string

|

The collection namespace, which includes the database name, a dot (`.`)
separator, and the collection name. For example: `<database>.<collection>`

|

yes  
  
`to`

|

string

|

The new name for the collection specified as a namespace, which includes the
database name, a dot (`.`) separator, and the new collection name. The new
name:

  * Must be unique if `dropTarget` is omitted or is set to `false`.

  * Can be the name of an existing collection in the same database if `dropTarget` is specified _and_ is set to `true` (that is, `dropTarget == true`).

|

yes  
  
`dropTarget`

|

boolean

|

Specifies whether or not to rename the collection to a name that already
exists in the database. Value can be `true` or `false`. The default value is
`false`, which means that the new name for the collection must be unique. If
`true`, overwrites the existing collection's data with data from the renamed
collection.

|

no  
  
## Output

The command returns the following output if it succeeds. You can verify the
results by running the commands in Verify Collection. If it fails, see
Troubleshoot Errors below for recommended solutions.

    
    
    { "ok" : 1 }  
      
  
## Examples

These examples use the following `databases` and `collections` in the storage
configuration:

    
    
    "databases" : [  
      
      {  
        "name": "multiCollDB",  
        "collections": [  
          {  
            "name": "air_airlines",  
            "dataSources": [{  
              "storeName" : "egS3Store",  
              "path" : "egData/air_airlines.json"  
            }]  
          },  
          {  
            "name": "airbnb",  
            "dataSources": [{  
              "storeName" : "sampleS3Store",  
              "path" : "json/airbnb/*"  
            }]  
          },  
          {  
            "name": "weather",  
            "dataSources": [{  
              "storeName" : "sampleS3Store",  
              "path" : "json/weather/*"  
            }]  
          }  
        ]  
      }  
    ]  
  
### Basic Example

The following `renameCollection` command renames the `air_airlines` collection
in the database named `multiCollDB` to `airlines`.

    
    
    use admin  
      
    db.runCommand({ "renameCollection": "multiCollDB.air_airlines", "to": "multiCollDB.airlines" })  
  
The previous command prints the following output:

    
    
    { "ok" : 1 }  
      
  
### `dropTarget` Example

The following `renameCollection` command:

  1. Renames the `weather` collection in the database named `multiCollDB` to `airbnb`, which is the name of an existing collection in the same database.

  2. Replaces `airbnb` collection data with the data in the `weather` collection.

    
    
    use admin  
      
    db.runCommand({ "renameCollection": "multiCollDB.weather", "to": "multiCollDB.airbnb", "dropTarget": true })  
  
The previous command prints the following output:

    
    
    { "ok" : 1 }  
      
  
The following command shows that the collection was successfully renamed:

    
    
    > show collections  
      
    airbnb  
    > db.runCommand({ "storageGetConfig" : 1 })  
    {  
           "ok" : 1,  
           "storage" : {  
                  "stores" : [  
                         {  
                           "name" : "egS3Store",  
                           "provider" : "s3",  
                           "region" : "us-east-2",  
                           "bucket" : "sbx-data-federation",  
                           "delimiter" : "/",  
                           "prefix" : ""  
                         }  
                  ],  
                  "databases" : [{  
                         "name" : "multiCollDB",  
                         "collections" : [{  
                           "name": "airbnb",  
                           "dataSources" : [  
                                  {  
                                         "storeName" : "egS3Store",  
                                         "path" : "/json/airbnb"  
                                  }  
                           ]  
                         }]  
                  }]  
           }  
    }  
  
## Verify Collection

You can verify that the command succeeded by running any of the following
commands:

    
    
    show collections  
      
    db.runCommand({ "storageGetConfig" : 1 })  
  
## Troubleshoot Errors

If the command fails, it returns one of the following errors:

    
    
    {  
      
     "ok": 0,  
     "errmsg": "renameCollection can only be run against the admin database”,  
     "code": 13,  
     "codeName": "Unauthorized"  
    }  
  
 **Solution:** Switch to the `admin` database and re-run the command. To
switch to the `admin` database, run the `use admin` command.

    
    
    {  
      
     "ok": 0,  
     "errmsg": "Invalid namespace specified '<ns>'",  
     "code": 73,  
     "codeName": "InvalidNamespace"  
    }  
  
 **Solution:** Check that the specified namespace (database or collection)
exists in the storage configuration.

    
    
    {  
      
     "ok": 0,  
     "errmsg": "Invalid target namespace: <namespace>",  
     "code": 73,  
     "codeName": "InvalidNamespace"  
    }  
  
 **Solution:** Ensure that the namespace (database or collection) specified
with the `to` field is valid.

    
    
    {  
      
     "ok": 0,  
     "errmsg": "target namespace exists",  
     "code": 48,  
     "codeName": "NamespaceExists"  
    }  
  
 **Solution:** Check that a collection with the specified name does not
already exist. Collection name must be unique if `dropTarget` is omitted or
set to `false`.

    
    
    {  
      
     "ok": 0,  
     "errmsg": "source namespace does not exist",  
     "code": 26,  
     "codeName": "NamespaceNotFound"  
    }  
  
 **Solution:** Check the database name is valid and exists in the storage
configuration.

    
    
    {  
      
     "ok": 0,  
     "errmsg": "cannot rename a collection created from a wildcard",  
     "code": 73,  
     "codeName": "InvalidNamespace"  
    }  
  
 **Solution:** Collections created by the wildcard collection function
(`collectionName()`) cannot be renamed.

← `create``drop` →

