Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Terminate a Serverless Instance

Share Feedback

On this page

  * Terminate One Serverless Instance

## Terminate One Serverless Instance

Atlas CLI

Atlas UI

## Note

If you enabled Termination Protection on your cluster, you must first disable
it.

To delete one serverless instance in the project you specify using the Atlas
CLI, run the following command:

    
    
    atlas serverless delete <instanceName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas serverless delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

Atlas terminates the serverless instance after completing any in-progress
deployment changes.

Atlas bills for the hours that the serverless instance was active. To learn
more about Atlas billing, see Manage Billing.

← Configure Serverless Instance BackupManage Global Clusters →

