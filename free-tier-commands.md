Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Commands Available Only in Free Clusters

Share Feedback

On this page

  * atlasSize

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

The following command is specific to Atlas free clusters:

## atlasSize

Returns the cumulative size across all databases in a free cluster for the
following database statistics:

    
    
    {  
      
      "totals": {  
      "collections": [number-total-collections],  
      "views": [number-total-views],  
      "objects": [number-total-objects],  
      "avgObjSize": [number-average-across-all],  
      "dataSize": [number-total-dataSize],  
      "storageSize": [number-total-storageSize],  
      "numExtents": [number-total-numExtents],  
      "indexes": [number-total-indexes],  
      "indexSize": [number-total-indexSize],  
      "fileSize": [number-total-fileSize],  
      "numDatabases": [number-total-databases],  
      "indexSize": [number-total-indexSize]  
    },  
      "atlasSize": [number-total-data-plus-total-index-size],  
      "ok": 1  
    }  
  
The `atlasSize` field represents the combination of the total size of data and
indexes in the cluster.

### Example Request

    
    
    db.runCommand({atlasSize:1})  
      
  
### Example Response

    
    
    {  
      
          "totals" : {  
            "collections" : 11,  
            "views" : 0,  
            "objects" : NumberLong(530025),  
            "avgObjSize" : 277.0923742138365,  
            "dataSize" : NumberLong(532890980),  
            "storageSize" : NumberLong(555319296),  
            "numExtents" : NumberLong(0),  
            "indexes" : 11,  
            "indexSize" : NumberLong(4792320),  
            "fileSize" : NumberLong(0),  
            "numDatabases" : 4  
          },  
          "atlasSize" : NumberLong(537683300),  
          "ok" : 1  
    }  
  
← Unsupported Commands in AtlasOplog Access →

