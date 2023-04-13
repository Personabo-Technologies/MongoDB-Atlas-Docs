Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `dropDatabase`

Share Feedback

On this page

  * Syntax
  * Parameters
  * Output
  * Example
  * Troubleshoot Errors

The `dropDatabase` command removes the specified database from the storage
configuration. If you drop a database that contains one or more collections,
the collections are also removed from the storage configuration.

## Syntax

    
    
    db.runCommand({ "dropDatabase": 1 })  
      
  
## Parameters

Parameter

|

Type

|

Description

|

Required?  
  
|||  
  
`1`

|

int

|

The flag to pass when dropping a database from the storage configuration.

|

yes  
  
## Output

The command prints the following output if the command succeeds or if there is
no database with the specified name to drop. To check whether the database was
dropped from the storage configuration, run the `show dbs` and
`storageGetConfig` commands. If the command prints errors, see Troubleshoot
Errors below for recommended solutions.

    
    
    { "ok" : 1 }  
      
  
## Example

The following example uses the `dropDatabase` command to drop a database named
`egS3Store` from the federated database instance storage configuration.

    
    
    use egS3Store  
      
    db.runCommand({ "dropDatabase": 1 })  
  
The previous command prints the following output:

    
    
    { "ok" : 1 }  
      
  
## Troubleshoot Errors

If the command fails, it prints the following error:

    
    
    {  
      
       ok: 0,  
       errmsg: “have to pass 1 as db parameter”,  
       code: 20,  
       codeName: "IllegalOperation"  
    }  
  
 **Solution:** Specify `1` as the parameter to the command.

← `drop``dropStore` →

