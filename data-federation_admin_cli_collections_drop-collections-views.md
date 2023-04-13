Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `drop`

Share Feedback

On this page

  * Syntax
  * Parameters
  * Output
  * Examples
  * Drop Collections Examples
  * Drop Views Example
  * Troubleshoot Errors

The `drop` command removes the specified collection or view from the federated
database instance storage configuration. Use the wildcard `"*"` to remove all
collections generated by the wildcard collection function (that is,
`collectionName()`), including the wildcard collection rule itself. You cannot
individually remove collections generated by the wildcard collection function.

## Syntax

Collection

Views

    
    
    db.runCommand({ "drop" : "<collection-name|*>" })  
      
  
## Parameters

Collection

Views

Parameter

|

Type

|

Description

|

Required?  
  
|||  
  
`<collection-name>`

|

string

|

The name of the collection to drop or the wildcard `"*"` . You can specify the
wildcard `"*"` to drop:

  * All collections generated by the wildcard collection function `collectionName()`

  * The wildcard collection rule

|

yes  
  
## Output

Collection

Views

The command prints the following output if it succeeds. You can verify the
results by running the `show collections` command. If the command fails, see
Troubleshoot Errors for recommended solutions.

    
    
    { "ok" : 1, "ns" : "<database>.<collection>", "nIndexesWas" : 0 }  
      
  
where:

  * `ns` reflects the collection namespace, which includes the database name, the dot (`.`) separator, and the collection name. For example: `<database>.<collection>`.

  * `nIndexesWas` reflects the number of indexes, the value of which is always `0` on Data Federation.

## Examples

### Drop Collections Examples

The following examples use the `drop` command to remove sample collections
that were mapped to the sample dataset, airbnb and weather, in the AWS S3
store.

#### Basic Example

The following example uses the `drop` command to remove a sample collection
named `airbnb` in a database named `sample` in the storage configuration.

    
    
    use sample  
      
    db.runCommand({ "drop" : "airbnb"})  
  
The previous command prints the following output:

    
    
    { "ok" : 1, "ns" : "sample.airbnb", "nIndexesWas" : 0 }  
      
  
#### Wildcard Example

The following example uses the `drop` command to remove the wildcard
collection function (`collectionName()`) and all collections created by the
wildcard collection function in a database named `sample` in the storage
configuration.

    
    
    use sample  
      
    db.runCommand ({ "drop" : "*" })  
  
The previous command prints the following output:

    
    
    { "ok" : 1, "ns" : "sample.*", "nIndexesWas" : 0 }  
      
  
### Drop Views Example

The following command removes a view named "listings" on the airbnb collection
in the `sample` database:

    
    
    use sample  
      
    db.runCommand({ "drop" : "listings" })  
  
The previous command returns the following output:

## Example

    
    
    { "ok" : 1, "ns" : "sample.listings", "nIndexesWas" : 0 }  
      
  
## Troubleshoot Errors

If the command fails, it returns one of the following errors.

 **Reason:** Namespace (database, collection, or view) does not exist.

    
    
    {  
      
       ok: 0,  
       errmsg: "ns not found",  
       code: 26,  
       codeName: "NamespaceNotFound"  
    }  
  
 **Solution:** Ensure that the namespace specified in the command is valid and
exists in the storage configuration. If necessary, use the `getStorageConfig`
command to retrieve the list of valid databases, collections, and views in the
storage configuration.

 **Reason:** Attempting to remove a collection created by the wildcard
collection function (`collectionName()`).

    
    
    {  
      
       ok: 0,  
       errmsg: "cannot drop a collection created from a wildcard",  
       code: 26,  
       codeName: "NamespaceNotFound"  
    }  
  
 **Solution:** Ensure that the collection you are dropping is not an
individual collection dynamically generated by the wildcard collection
function (`collectionName()`). Data Federation does not support dropping
individual collections generated by the wildcard collection function.

← `renameCollection``dropDatabase` →
