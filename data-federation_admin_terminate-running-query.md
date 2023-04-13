Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Terminate a Running Federated Database Instance Query

Share Feedback

On this page

  * Syntax
  * Options
  * Output
  * Examples

You can terminate long-running queries using the killOp command. For more
information, see killOp. In Atlas Data Federation:

  * The `op` parameter value is an ObjectId.

  * The `comment` parameter is not supported.

If you are an Admin user, you can kill any query on a federated database. The
user who issued the query can also terminate the query. To run this command,
use db.runCommand(). You must run killOp against the `admin` database.

## Syntax

    
    
    db.runCommand({ "killOp": 1, "op":  ObjectId(<hexadecimal>) })  
      
  
## Options

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`op`

|

ObjectId

|

Unique identifier, in ObjectId format, of the operation to terminate. You can
use $currentOp to retrieve the `opid` of the operation to terminate.

|

Required  
  
## Output

killOp returns the following if it succeeds in marking the specified operation
for termination:

    
    
    { "info" : "attempting to kill op", "ok" : 1 }  
      
  
Note that the output is the same whether or not the operation being terminated
is currently running. You can use $currentOp to verify that the operation was
terminated.

## Examples

For the example below, suppose a query with `opid` value of
`ObjectId("1635fad364c529820c6f9e76")` is running. The following command
terminates this query.

    
    
    use admin  
      
    db.runCommand({ "killOp": 1, "op": ObjectId("1635fad364c529820c6f9e76") })  
  
The previous command returns the following:

    
    
    { "info" : "attempting to kill op", "ok" : 1 }  
      
  
← Determine Status of Queries Against Federated Database InstancesRetrieve
Federated Database Instance Query History →

