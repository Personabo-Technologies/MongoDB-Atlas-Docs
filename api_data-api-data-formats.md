Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Data API Data Formats

Share Feedback

On this page

  * BSON Types
  * Array
  * Binary
  * Date
  * Decimal128
  * Document
  * Double
  * Int32
  * Int64
  * MaxKey
  * MinKey
  * ObjectId
  * Regular Expression
  * Timestamp

MongoDB stores data in a format called BSON, which is similar to a JSON object
in structure but supports additional data types and uses a binary encoding.
BSON is efficient for computers but is not human readable, so you can't work
with it directly.

Instead, the Data API uses two formats to represent data in requests and
responses:

  * The **JSON** format uses standard types that any tool can parse and understand. However, JSON cannot represent all BSON types, so JSON responses may lose type information for some fields. For example, BSON has distinct types for 32-bit integers and 64-bit floats, but a JSON response represents both as a `number`.

  * The **EJSON** format, short for MongoDB Extended JSON, is a superset of standard JSON that uses structured fields to represent BSON data that don't have corresponding JSON types. This fully represents your data but requires your client to understand how to work with EJSON.

## Example

This document can be represented in either JSON or EJSON shows BSON types
represented in JSON and EJSON:

EJSON

JSON

    
    
    {  
      
       "Name": "Mango",  
       "Year": { "$numberLong": "2022" },  
       "Weight": { "$numberDecimal": "9823.1297" },  
       "Date": { "$date": { "$numberLong": "1641954803067" } }  
    }  
  
You define a single default return type for all generated Data API endpoints
and individually for each custom endpoint. Incoming requests can also specify
a preferred data format that overrides the default using an `Accept` header.
To learn more, see Choose a Response Data Format.

## BSON Types

This sections lists the BSON types that the Data API supports and shows how
each type is represented in JSON and EJSON format.

### Array

EJSON

|

JSON  
  
|  
      
    
    | [ <elements> ]  
      
      
    
    | [ <elements> ]  
      
  
### Binary

EJSON

|

JSON  
  
|  
      
    
    | {  
      
       "$binary": {  
          "base64": "e67803a39588be8a95731a21e27d7391",  
          "subType": "05"  
       }  
    }  
      
    
    | {  
      
       "Subtype": 5,  
       "Data": "e67803a39588be8a95731a21e27d7391"  
    }  
  
### Date

EJSON

|

JSON  
  
|  
      
    
    | {  
      
       "$date": {  
          "$numberLong": "1641954803067"  
       }  
    }  
      
    
    | "2022-01-12T02:33:23.067Z"  
      
  
### Decimal128

EJSON

|

JSON  
  
|  
      
    
    | { "$numberDecimal": "9823.1297" }  
      
      
    
    | "9823.1297"  
      
  
### Document

EJSON

|

JSON  
  
|  
      
    
    | { <content> }  
      
      
    
    | { <content> }  
      
  
### Double

EJSON

|

JSON  
  
|  
      
    
    | {  
      
       "$numberDouble": "10.5"  
    }  
      
    
    | 10.5  
      
  
### Int32

EJSON

|

JSON  
  
|  
      
    
    | {"$numberInt":"10"}  
      
      
    
    | 10  
      
  
### Int64

EJSON

|

JSON  
  
|  
      
    
    | {"$numberLong":"50"}  
      
      
    
    | 50  
      
  
### MaxKey

EJSON

|

JSON  
  
|  
      
    
    | { "$maxKey": 1 }  
      
      
    
    | {}  
      
  
 _No JSON equivalent_  
  
### MinKey

EJSON

|

JSON  
  
|  
      
    
    | { "$minKey": 1 }  
      
      
    
    | {}  
      
  
 _No JSON equivalent_  
  
### ObjectId

EJSON

|

JSON  
  
|  
      
    
    | {  
      
       "$oid":"5d505646cf6d4fe581014ab2"  
    }  
      
    
    | "5d505646cf6d4fe581014ab2"  
      
  
### Regular Expression

EJSON

|

JSON  
  
|  
      
    
    | {  
      
       "$regularExpression": {  
          "pattern":"^H",  
          "options":"i"  
       }  
    }  
      
    
    | {  
      
       "Pattern": "^H",  
       "Options": "i"  
    }  
  
### Timestamp

EJSON

|

JSON  
  
|  
      
    
    | {  
      
       "$timestamp": {  
          "t":1565545664,  
          "i":1  
        }  
    }  
      
    
    | {  
      
       "T": 1565545664,  
       "I": 1  
    }  
  
← Data API ExamplesAtlas CLI →

