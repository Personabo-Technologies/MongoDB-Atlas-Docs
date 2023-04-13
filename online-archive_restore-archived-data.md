Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Restore Archived Data

Share Feedback

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

You can restore archived data to your Atlas cluster. You can use the alternate
syntax that Atlas Data Federation provides for the $merge pipeline stage to
move the data back into the same or different Atlas cluster, database, or
collection within the same Atlas project.

## Note

Ensure that your cluster is adequately provisioned for the amount of data that
will be restored from your archive so that it doesn't run out of space during
or after restoration of archived data. Contact Get Help with Atlas for
additional technical guidance on setting up the size of the oplog or for
troubleshooting any space issues on your Atlas cluster.

This page describes how to restore using the `$merge` pipeline stage.

## Procedure

1

### Pause the online archive associated with the collection whose archived
data you wish to restore.

See Pause and Resume Archiving for more information.

2

### Connect to Online Archive using the connection string.

See Connect to Online Archive for more information.

3

### Use `$merge` to move the data from your archive to your Atlas cluster.

To learn more about the `$merge` pipeline stage syntax and usage for moving
data back into your Atlas cluster, see the $merge pipeline stage.

## Example

Consider the following documents in an S3 archive:

    
    
    {  
      
      "_id" : 1,  
      "item": "cucumber",  
      "source": "nepal",  
      "released": ISODate("2016-05-18T16:00:00Z")  
    }  
    {  
      "_id" : 2,  
      "item": "miso",  
      "source": "canada",  
      "released": ISODate("2016-05-18T16:00:00Z")  
    }  
    {  
      "_id" : 3,  
      "item": "oyster",  
      "source": "luxembourg",  
      "released": ISODate("2016-05-18T16:00:00Z")  
    }  
    {  
      "_id" : 4,  
      "item": "mushroom",  
      "source": "ghana",  
      "released": ISODate("2016-05-18T16:00:00Z")  
    }  
  
Suppose the `$merge` syntax for restoring these documents into the Atlas
cluster identifies documents based on the `item` and `source` fields during
the `$merge` stage.

    
    
    db.<collection>.aggregate([  
      
      {  
        "$merge": {  
          "into": {  
            "atlas": {  
              "clusterName": "<atlas-cluster-name>",  
              "db": "<db-name>",  
              "coll": "<collection-name>"  
            }  
          },  
          "on": [ "item", "source" ],  
          "whenMatched": "keepExisting",  
          "whenNotMatched": "insert"  
        }  
      }  
    ])  
  
In this example, when an archived document matches a document on the Atlas
cluster on those two fields, Atlas keeps the existing document in the cluster
because the copy of the document on the Atlas cluster is more recent than the
copy of the document in the archive. When an archived document doesn't match
any document in the Atlas cluster, Atlas inserts the document into the
specified collection on the Atlas cluster.

When restoring data back into the Atlas cluster, the archived data might have
duplicate `_id` fields. For this example, we can include a `$sort` stage for
sorting on the `_id` and `released` fields before the `$merge` stage to ensure
that Atlas chooses the documents with the recent date if there are duplicates
to resolve.

    
    
    db.<collection>.aggregate([  
      
      {  
        $sort: {  
          "_id": 1,  
          "released": 1,  
        }  
      },  
      {  
        "$merge": {  
          "into": {  
            "atlas": {  
              "clusterName": "<atlas-cluster-name>",  
              "db": "<db-name>",  
              "coll": "<collection-name>"  
            }  
          },  
          "on": [ "item", "source" ],  
          "whenMatched": "keepExisting",  
          "whenNotMatched": "insert"  
        }  
      }  
    ])  
  
To learn more about resolving duplicate fields, see the $merge considerations.

4

### Verify data in the Atlas cluster and delete the online archive.

See Delete an Online Archive for more information.

← Back Up Online Archive DataDownload Query Logs →

