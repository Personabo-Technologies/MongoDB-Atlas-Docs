Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Custom Database Roles

Share Feedback

On this page

  * Create or Update a Custom Database Role

You can create custom roles in Atlas when the built-in roles don't include
your desired set of privileges. Atlas applies each database user's custom
roles together with:

  * Any built-in roles you assign when you add a database user or modify a database user.

  * Any specific privileges you assign when you add a database user or modify a database user.

You can assign multiple custom roles to each database user.

## Note

### Free Cluster, Shared Cluster, and Serverless Instance Limitation

Changes to custom roles might take up to 30 seconds to deploy in `M0` free
clusters, `M2/M5` shared clusters, and serverless instances.

## Create or Update a Custom Database Role

To create or update a custom database role, specify the `spec.customRoles`
parameters in the `AtlasProject` Custom Resource.

 **Example**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
     name: my-project  
     labels:  
       app.kubernetes.io/version: 1.6.0  
    spec:  
     name: Test Atlas Operator Project  
     connectionSecretRef:  
      name: my-atlas-key  
     customRoles:  
      - roleName: "my-role"  
        actions:  
         - action: "my-action"  
           resources:  
            - cluster: false  
              collection: "my-collection"  
              db: "my-database"  
        inheritedRoles:  
         - db: "my-database"  
           role: "clusterMonitor"  
  
To learn more about the configuration parameters available from the API, see
the Atlas Custom Database Roles API.

← Configure TeamsEncrypt Data Using a Key Management Service →

