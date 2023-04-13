Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `dropStore`

Share Feedback

On this page

  * Syntax
  * Parameters
  * Output
  * Example
  * Troubleshoot Errors

The `dropStore` command removes a federated database instance store from the
federated database instance storage configuration. If existing collections
reference the federated database instance store you want to remove, the
command fails and returns a list of the dependent collections.

## Syntax

    
    
    db.runCommand({ dropStore: "<store-name>" })  
      
  
## Parameters

Parameter

|

Type

|

Description

|

Required?  
  
|||  
  
`dropStore`

|

string

|

Name of the federated database instance store to remove from the federated
database instance storage configuration.

|

yes  
  
## Output

The command prints the following output if it succeeds. If the command fails,
see Troubleshoot Errors for recommended solutions.

    
    
    { "ok" : 1 }  
      
  
## Example

The following example uses the `dropStore` command to remove the federated
database instance store `myStore` from the federated database instance storage
configuration.

    
    
    use sample  
      
    db.runCommand({ dropStore: "myStore" })  
  
The previous command prints the following output:

    
    
    { "ok" : 1 }  
      
  
## Troubleshoot Errors

If the command fails, it returns one of the following errors.

 **Reason:** The specified federated database instance store has dependent
collections and can't be removed.

    
    
    {  
      
      "ok" : 0,  
      "errmsg" : "store has dependent collections: <database.collection>,<database.collection>,<...>",  
      "code" : 2,  
      "codeName" : "BadValue"  
    }  
  
 **Solution:** First drop the dependent collections, then re-run the
`dropStore` command.

← `dropDatabase`Manage Namespace Metadata Catalog for Wildcard Collections →

