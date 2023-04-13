Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `listStores`

Share Feedback

On this page

  * Syntax
  * Parameters
  * Output
  * Example

The `listStores` command lists all federated database instance stores in the
federated database instance storage configuration.

## Syntax

    
    
    db.runCommand({ listStores: 1 })  
      
  
## Parameters

Parameter

|

Type

|

Description

|

Required?  
  
|||  
  
`listStores`

|

int

|

Indicates that all federated database instance stores be listed.

Value must be `1`.

|

yes  
  
## Output

The command prints the following output if it succeeds.

    
    
    {  
      
      "ok": 1,  
      "cursor": {  
        "firstBatch": [  
          {  
            "name": "<store-name>",  
            "provider": "s3",  
            "region": "<region-name>",  
            "bucket": "<bucket-name>",  
            "delimiter": "<delimiter>",  
            "prefix": "<prefix>"  
          },  
          {  
            "name": "<store-name>",  
            "provider": "atlas",  
            "clusterName": "<cluster-name>",  
            "projectId": "<project-id>"  
          },  
          ...  
        ],  
        "id": NumberLong(0),  
        "ns": "<database>.$cmd.listStores"  
      }  
    }  
  
## Example

The following example uses the `listStores` command to list all federated
database instance stores in an federated database instance storage
configuration.

    
    
    use sample  
      
    db.runCommand({ listStores: 1 })  
  
The previous command prints the following:

    
    
    {  
      
      "ok": 1,  
      "cursor": {  
        "firstBatch": [  
          {  
            "name": "s3store",  
            "provider": "s3",  
            "region": "us-east-1",  
            "bucket": "my-bucket",  
            "delimiter": "/",  
            "prefix": ""  
          },  
          {  
            "name" : "atlasStore",  
            "provider" : "atlas",  
            "clusterName" : "myTestCluster",  
            "projectId" : "<project-id>"  
          }  
        ],  
        "id": NumberLong(0),  
        "ns": "sample.$cmd.listStores"  
      }  
    }  
  
← `createStore``create` →

