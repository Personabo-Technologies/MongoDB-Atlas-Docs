Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Storage Configuration Commands

Share Feedback

On this page

  * `storageGetConfig`
  * `storageSetConfig`
  * `storageGenerateConfig`
  * `storageValidateConfig`

## `storageGetConfig`

The `storageGetConfig` command returns the current federated database instance
configuration.

    
    
    db.runCommand( { "storageGetConfig" : 1 } )  
      
  
To learn more about this command, see Retrieve Federated Database Instance
Configuration.

## `storageSetConfig`

The `storageSetConfig` command replaces the current federated database
instance configuration with a JSON document.

    
    
    db.runCommand( { "storageSetConfig" : <config> } )  
      
  
To learn more about this command, see Set or Update Federated Database
Instance Configuration.

## `storageGenerateConfig`

The `storageGenerateConfig` command generates a configuration for your
federated database instance in JSON format.

    
    
    db.runCommand( { "storageGenerateConfig" : 1 } )  
      
  
To learn more about this command, see Generate Federated Database Instance
Configuration.

## `storageValidateConfig`

The `storageValidateConfig` command validates the given federated database
instance configuration.

    
    
    db.runCommand( { "storageValidateConfig" : <config> } )  
      
  
To learn more about this command, see Validate Federated Database Instance
Configuration.

← Role Management CommandsSupported Aggregation Pipeline Stages and Operators
→

