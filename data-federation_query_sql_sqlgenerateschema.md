Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `sqlGenerateSchema`

Share Feedback

On this page

  * Syntax
  * Parameters
  * Output
  * Examples
  * Basic Example
  * Generate and Set Schema Example
  * Errors

The `sqlGenerateSchema` command generates a SQL schema for the specified
collection or view.

## Syntax

    
    
    db.runCommand({sqlGenerateSchema: 1, sampleNamespaces: [<namespace>], sampleSize: <int>, setSchemas: true|false})  
      
  
## Parameters

Parameter

|

Type

|

Description

|

Necessity  
  
|||  
  
`sampleNamespaces`

|

array of strings

|

Specifies the comma-separated list of namespaces for which to generate
schemas. A namespace includes the database name, a dot (.) separator, and the
collection or view name (i.e. `<database>.<collection>|<view>`). To generate
schemas for all the collections in a database, specify `*` instead of the
collection or view name (i.e. `<database>.*`). If omitted, generates schemas
for all collections and views in the current database.

|

Optional  
  
`sampleSize`

|

integer

|

Specifies the number of documents to use as a sample to create the schema. If
omitted, defaults to `1000`.

|

Optional  
  
`setSchemas`

|

boolean

|

Specifies whether or not to store the generated schema for the collection or
view. Value can be one of the following:

  * `true` to store the schema. If a schema already exists for the collection or view, overwrite the existing schema.

  * `false` to not store the schema.

If omitted, defaults to `false`.

|

Optional  
  
## Output

The command returns the following if the command succeeds.

    
    
    {  
      
          "ok" : 1,  
          "schemas" : [  
            {  
                  "databaseName" : "<database-name>",  
                  "namespaces" : [  
                    {  
                          "name" : "<collection-name>",  
                          "schema" : {  
                            "version" : NumberLong(1),  
                            "jsonSchema" : {}  
                          }  
                    }  
                  ]  
            },  
            ...  
          ]  
    }  
  
The `schemas` object contains the following fields.

Parameter

|

Type

|

Description  
  
||  
  
`databaseName`

|

string

|

Name of the database.  
  
`namespaces`

|

array of objects

|

Name and generated schema of each collection or view.  
  
`namespaces.name`

|

string

|

Name of the collection or view.  
  
`namespaces[n].schema`

|

document

|

Schema of the collection or view.  
  
`namespaces[n].schema.version`

|

integer

|

Format version of the schema. Value is always 1.  
  
`namespaces[n].schema.jsonSchema`

|

document

|

JSON schema of the collection or view. The JSON schema can contain the
following fields:

  * `bsonType`

  * `properties`

  * `items`

To learn more about these fields, see JSON Schema Keywords.  
  
If you set the schema for the collection or view using the `setSchemas`
option, you can verify that the command succeeded by running the
`sqlGetSchema` command. The `sqlGetSchema` command `metadata.description`
should contain the following value:

    
    
    "set using sqlGenerateSchema with setSchemas = true"  
      
  
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
  
The examples below use the `sqlGenerateSchema` command to generate a schema
for the above collection.

## Basic Example

The following command generates a schema for the collection named
`sampleDB.egData` in the storage configuration. The command uses two randomly
selected documents from the collection to create the schema because the
`sampleSize` is `2`. The command does not set the schema for the collection
because the `setSchemas` option is not specified with the command and defaults
to `false`.

    
    
    db.runCommand({sqlGenerateSchema: 1, sampleNamespaces: ["sampleDB.egData"], sampleSize: 2})  
      
  
The previous command returns the following output. To learn more about the
fields in the output, see Output.

    
    
    {  
      
          "ok" : 1,  
          "schemas" : [  
            {  
                  "databaseName" : "sampleDB",  
                  "namespaces" : [  
                    {  
                          "name" : "egData",  
                          "schema" : {  
                            "version" : NumberLong(1),  
                            "jsonSchema" : {  
                                  "bsonType" : [  
                                    "object"  
                                  ],  
                                  "properties" : {  
                                    "a" : {  
                                          "bsonType" : [  
                                            "object"  
                                          ],  
                                          "properties" : {  
                                            "b" : {  
                                                  "bsonType" : [  
                                                    "object"  
                                                  ],  
                                                  "properties" : {  
                                                    "c" : {  
                                                          "bsonType" : [  
                                                            "array"  
                                                          ],  
                                                          "items" : {  
                                                            "bsonType" : [  
                                                                  "int"  
                                                            ]  
                                                          }  
                                                    }  
                                                  }  
                                            }  
                                          }  
                                    },  
                                    "s" : {  
                                          "bsonType" : [  
                                            "int"  
                                          ]  
                                    }  
                                  }  
                            }  
                          }  
                    }  
                  ]  
            }  
          ]  
    }  
  
## Generate and Set Schema Example

The following command generates a schema for the collection named
`sampleDB.egData` in the storage configuration. The command uses up to 1000
documents in the collection to create the schema because the `sampleSize`
option is not specified with the command and defaults to `1000`. The command
sets the generated schema as the schema to use for the collection because the
`setSchemas` option is set to `true`.

    
    
    db.runCommand({sqlGenerateSchema: 1, sampleNamespaces: ["sampleDB.egData"], setSchemas: true})  
      
  
The previous command returns the following output. To learn more about the
fields in the output, see Output.

    
    
    {  
      
          "ok" : 1,  
          "schemas" : [  
            {  
                  "databaseName" : "sampleDB",  
                  "namespaces" : [  
                    {  
                          "name" : "egData",  
                          "schema" : {  
                            "version" : NumberLong(1),  
                            "jsonSchema" : {  
                                  "bsonType" : [  
                                    "object"  
                                  ],  
                              "properties" : {  
                                    "a" : {  
                                      "bsonType" : [  
                                            "object"  
                                      ],  
                                      "properties" : {  
                                            "b" : {  
                                              "bsonType" : [  
                                                    "object",  
                                                    "array"  
                                              ],  
                                              "properties" : {  
                                                    "c" : {  
                                                      "bsonType" : [  
                                                            "array",  
                                                            "string",  
                                                            "object",  
                                                            "null"  
                                                      ],  
                                                      "properties" : {  
                                                            "d" : {  
                                                              "bsonType" : [  
                                                                    "int"  
                                                              ]  
                                                            }  
                                                      },  
                                                        "items" : {  
                                                                "bsonType" : [  
                                                                        "int"  
                                                                ]  
                                                        }  
                                                }  
                                              },  
                                              "items" : {  
                                                      "bsonType" : [  
                                                        "int"  
                                                        ]  
                                                }  
                                        }  
                                      }  
                                },  
                                "s" : {  
                                      "bsonType" : [  
                                        "int",  
                                        "object"  
                                      ]  
                                }  
                              }  
                        }  
                }  
              ]  
            }  
          ]  
    }  
  
## Errors

The command returns the following error if the command fails:

    
    
     "failedNamespaces": [  
      
       {  
         "namespace" : "<db.ns>",  
         "error" : "no documents found in sample namespace"  
       }  
    ]  
  
The above error is returned if the specified namespaces do not exist in the
storage configuration or are empty. This error is also returned if the schema
could not be set for a given namespace.

← SQL Schema Format`sqlSetSchema` →

