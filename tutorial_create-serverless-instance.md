Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Serverless Instance

Share Feedback

This tutorial takes you through the steps to create a new Atlas serverless
instance.

To convert your existing shared cluster to a serverless instance, see Convert
a Shared Cluster to a Serverless Instance.

## Procedure

Atlas CLI

Atlas UI

To create one serverless instance in the project you specify using the Atlas
CLI, run the following command:

    
    
    atlas serverless create <instanceName> [options]  
      
  
To monitor the status of a serverless instance using the Atlas CLI, run the
following command:

    
    
    atlas serverless watch <instanceName> [options]  
      
  
The `watch` command checks the serverless instance's state periodically until
the instance reaches an idle state. Once the instance reaches the expected
state, the command prints `Instance available`. You can interrupt the
command's polling at any time with `CTRL` \+ `C`.

To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas serverless create and atlas serverless
watch.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Create a ClusterCreate a Global Cluster →

