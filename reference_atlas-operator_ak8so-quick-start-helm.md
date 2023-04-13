Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Helm Charts Quick Start

Share Feedback

On this page

  * Prerequisites
  * Procedure
  * Register for an Atlas account or log in.
  * Create API keys for your organization.
  * Deploy Atlas Kubernetes Operator.
  * Deploy the Atlas database deployment.
  * Check the status of your database user.
  * Retrieve the secret that Atlas Kubernetes Operator created to connect to the database deployment.

You can use Atlas Kubernetes Operator to manage resources in Atlas without
leaving Kubernetes. This tutorial demonstrates how to create your first
cluster in Atlas from Helm Charts with Atlas Kubernetes Operator.

## Note

### Would you prefer to start without Helm?

To create your first cluster in Atlas from Kubernetes configuration files with
Atlas Kubernetes Operator, see Quick Start.

## Prerequisites

This tutorial requires:

  * A running Kubernetes cluster with nodes running processors with the x86-64, AMD64, or ARM64 architecture.

You can access the Atlas Kubernetes Operator project on GitHub:

  * https://github.com/mongodb/mongodb-atlas-kubernetes

## Procedure

## Important

### Custom Resources Definitions Take Priority

Atlas Kubernetes Operator uses custom resource configuration files to manage
your Atlas configuration. Each custom resource definition overrides settings
specified in other ways such as in the Atlas UI. If you delete a custom
resource, Atlas Kubernetes Operator deletes the object from Atlas unless you
use annotations to skip deletion. To learn more, see the Create and Update
Process and the Delete Process.

1

### Register for an Atlas account or log in.

Register a new Atlas Account or Log in to Your Atlas Account.

2

### Create API keys for your organization.

## Note

You need the following public API key, private API key, and the organization
ID information to configure Atlas Kubernetes Operator access to Atlas.

Create an API Key in an Organization and configure the API Access List.

You need the following public API key, private API key, and the organization
ID information to configure Atlas Kubernetes Operator access to Atlas.

  * If you want Atlas Kubernetes Operator to create a new Atlas project, Create an API Key in an Organization and configure the API Access List.

## Important

You must assign the API key the Organization Project Creator organization role
or higher.

  * If you want to work with an existing Atlas project, Create an API Key for a Project and configure the API Access List.

## Important

You must assign the API key the Project Owner project role.

3

### Deploy Atlas Kubernetes Operator.

Run one of the following sets of commands:

  * If you want Atlas Kubernetes Operator to watch all namespaces in the Kubernetes cluster, run the following commands:
    
        helm repo add mongodb https://mongodb.github.io/helm-charts  
      
    helm install atlas-operator --namespace=atlas-operator --create-namespace mongodb/mongodb-atlas-operator  
  
  * If you want Atlas Kubernetes Operator to watch only its own namespace, set the `--watchNamespaces` flag to its own namespace, and run the following command:

## Note

You can set the `--watchNamespaces` flag only to its own namespace. Setting
the `--watchNamespaces` flag to any other namespace is currently unsupported.

    
        helm install atlas-operator --namespace=atlas-operator --set watchNamespaces=atlas-operator --create-namespace mongodb/mongodb-atlas-operator  
      
  

4

### Deploy the Atlas database deployment.

The `--set` flags in the following example override the `Values.yaml` file
values with your Atlas project name, organization ID, and API keys.

## Note

`mongodb/atlas-deployment` references the name of a chart in the repository.

Run the following command:

    
    
    helm install atlas-deployment \  
      
    mongodb/atlas-deployment \  
    --namespace=my-cluster \  
    --create-namespace \  
    --set project.atlasProjectName='My Project' \  
    --set atlas.orgId='<orgid>' \  
    --set atlas.publicApiKey='<publicKey>' \  
    --set atlas.privateApiKey='<privateApiKey>'  
  
Alternatively, you can clone the helm-charts project on GitHub, edit the
`Values.yaml` file directly, and add your local directory with the following
command:

    
    
    helm repo add mongodb <your-updated-helm-charts-directory>  
      
  
To learn more about the available parameters, see `AtlasDeployment` Custom
Resource.

To create a serverless instance, see the serverless instance example.

5

### Check the status of your database user.

Run the following command until you recieve a `True` response, which indicates
the database user is ready:

## Note

The `AtlasDatabaseUser` Custom Resource waits until the database deployment is
ready. Creating a new database deployment can take up to 10 minutes.

    
    
    kubectl -n my-cluster get atlasdatabaseusers atlas-deployment-admin-user -o=jsonpath='{.status.conditions[?(@.type=="Ready")].status}'  
      
  
6

### Retrieve the secret that Atlas Kubernetes Operator created to connect to
the database deployment.

Run the following command:

## Important

The following command requires `jq` 1.6 or higher.

    
    
    kubectl -n my-cluster get secret my-project-atlas-atlas-cluster-admin-user -o json | jq -r '.data | with_entries(.value |= @base64d)';  
      
  
## Note

Your connection strings will differ from the following example.

    
    
    {  
      
       "connectionStringStandard": "mongodb://admin-user:%25SomeLong%25password$foradmin@atlas-cluster-shard-00-00.nlrvs.mongodb.net:27017,atlas-cluster-shard-00-01.nlrvs.mongodb.net:27017,atlas-cluster-shard-00-02.nlrvs.mongodb.net:27017/?ssl=true&authSource=admin&replicaSet=atlas-11q9bn-shard-0",  
       "connectionStringStandardSrv": "mongodb+srv://admin-user:%25SomeLong%25password$foradmin@atlas-cluster.nlrvs.mongodb.net",  
       "password": "%SomeLong%password$foradmin",  
       "username": "admin-user"  
    }  
  
You can use this secret in your application:

    
    
    containers:  
      
     - name: test-app  
       env:  
         - name: "CONNECTION_STRING"  
           valueFrom:  
             secretKeyRef:  
               name: my-project-atlas-atlas-cluster-admin-user  
               key: connectionStringStandardSrv  
  
← Quick StartCompatibility →

