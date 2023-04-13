Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `catalogInfo`

Share Feedback

On this page

  * Syntax
  * Usage
  * Output
  * Example

The `catalogInfo` command returns an array of the stores and the ISODate when
the namespace metadata in the catalog was last updated.

## Syntax

    
    
    db.runCommand({ "catalogInfo" : 1, "stores": ["<storeName>"] })  
      
  
## Usage

To retrieve the last updated timestamp for all the stores, run the following
command:

    
    
    db.runCommand({ "catalogInfo" : 1 })  
      
  
To retrieve the last updated timestamp for a specific store, run the following
command:

    
    
    db.runCommand({ "catalogInfo" : 1, "stores": ["<storeName>"] })  
      
  
To retrieve the last updated timestamp for a list of stores, run the following
command:

    
    
    db.runCommand({ "catalogInfo" : 1, "stores": ["<storeName>",...] })  
      
  
## Output

The command returns output similar to the following if the command succeeds:

    
    
    {  
      
           "ok" : 1,  
           "stores" : [  
                  {  
                         "<storeName>" : ISODate("<date>")  
                  }  
           ]  
    }  
  
where:

  * `storeName` is the name of the S3 store

  * `date` is the date and timestamp in ISODate format

## Example

The following command returns the last updated date and timestamp for all the
stores.

    
    
    db.runCommand({"catalogInfo":1})  
      
  
The previous command returns the following output:

    
    
    {  
      
           "ok" : 1,  
           "stores" : [  
                  {  
                         "s3store" : ISODate("2020-03-25T12:35:32.165Z")  
                  },  
                  {  
                         "egS3Store" : ISODate("2020-03-25T12:35:32.165Z")  
                  }  
           ]  
    }  
  
← Manage Namespace Metadata Catalog for Wildcard Collections`updateCatalog` →

