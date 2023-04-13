Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `updateCatalog`

Share Feedback

On this page

  * Syntax
  * Options
  * Usage
  * Output
  * Example

The `updateCatalog` command updates the namespace metadata in the catalog. You
can verify by running the `catalogInfo` command, which shows the ISODate when
the catalog was last updated. If you have a large federated database instance
store, it may take a while to update the catalog.

## Syntax

    
    
    db.runCommand({ "updateCatalog" : 1, "stores": ["<storeName>"], "background" : true })  
      
  
## Options

Option

|

Type

|

Description

|

Necessity  
  
|||  
  
`background`

|

boolean

|

Flag to run command in the background. If omitted, defaults to `false`. When
set to `true`, Atlas Data Federation runs the command in the background.

    
    
    | { "background" : true }  
      
  
Optional  
  
`stores`

|

array of strings

|

Names of the stores for which to update the catalog. If omitted, Atlas Data
Federation updates the catalog for all the stores in the storage
configuration. If specified, Atlas Data Federation updates the catalog for the
specified stores only. Atlas Data Federation returns an error if a specified
store does not use a catalog.

|

Optional  
  
## Usage

To update the catalog for all the stores in the storage configuration, run the
following command:

    
    
    db.runCommand({ "updateCatalog" : 1 })  
      
  
The previous command runs in the foreground and is similar to running the
command with `background` set to `false`.

To update the catalog for all the stores in the storage configuration in the
background, run the following command:

    
    
    db.runCommand({ "updateCatalog" : 1, "background" : true })  
      
  
To update the catalog for a list of stores in the background, run the
following command:

    
    
    db.runCommand({ "updateCatalog" : 1, "stores": ["<storeName>",...], "background" : true })  
      
  
## Output

The command returns the following output:

    
    
    { "ok" : 1 }  
      
  
## Example

The following command updates the namespace metadata in the catalog:

    
    
    db.runCommand({ "updateCatalog" : 1 })  
      
  
The previous command returns the following output:

    
    
    { "ok" : 1 }  
      
  
← `catalogInfo`Manage Private Endpoints →

