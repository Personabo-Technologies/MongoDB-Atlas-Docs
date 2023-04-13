Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Generate Wildcard Collections

Share Feedback

You can dynamically generate collection names that map to data in your Atlas
cluster. To dynamically generate collection names, specify the wildcard, `*`,
as the value for the collection name setting in your federated database
instance storage configuration.

You can use the storageSetConfig command to configure the settings for
generating wildcard (`*`) collections.

For the Atlas data store, you can generate the following wildcard collections
and databases in your federated database instance storage configuration:

  * Wildcard collections for a specific database

  * Wildcard databases with one wildcard collection

You can also dynamically generate collection names that match a regex pattern.

Wildcard Collections

Wildcard Databases

To generate wildcard collections in your federated database instance storage
configuration that map to data in your Atlas cluster, configure the following
settings in your federated database instance storage configuration:

  * Specify `*` as the value for the `databases.[n].collections.[n].name` field.

  * Omit the `databases.[n].collections.[n].dataSources.[n].collection` field.

  *  _Optional_. Use the `databases.[n].collections.[n].dataSources.[n].collectionRegex` field to generate wildcard collection names that match a regex pattern.

## Example

    
    
    "databases" : [  
      
      {  
        "name" : "<db-name>",  
        "collections" : [  
          {  
            "name" : "*",  
            "dataSources" : [  
              {  
                "storeName" : "<atlas-store-name>",  
                "database" : "<atlas-db-name>",  
                "collectionRegex" : "<regex-pattern>"  
              }  
            ]  
          }  
        ]  
      }  
    ]  
  
You can also use the `create` administration command and the federated
database instance User Interface to configure the settings for generating
wildcard collections.

← Create From the UIHTTP URL →

